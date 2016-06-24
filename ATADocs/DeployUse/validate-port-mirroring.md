---
# required metadata

title: ポート ミラーリングの検証 | Microsoft Advanced Threat Analytics
description: ポート ミラーリングが適切に構成されていることを検証する方法について説明します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ポート ミラーリングの検証
> [!NOTE] この記事は、ATA 簡易ゲートウェイではなく、ATA ゲートウェイを展開する場合にのみ該当します。 ATA ゲートウェイを使用する必要があるかどうかの確認については、「[展開における適切なゲートウェイの選択](/advanced-threat-analytics/plan-design/ata-capacity-planning#Choosing-the-right-gateway-type-for-your-deployment)」を参照してください。
 
次の手順は、ポート ミラーリングが適切に構成されていることを検証するためのプロセスについて説明しています。 ATA が正常に機能するためには、ATA ゲートウェｲがドメイン コントローラーとのトラフィックを認識できる必要があります。 ATA で使用される主なデータ ソースは、ドメイン コントローラーとのネットワーク トラフィックの詳細なパケット検査です。 ATA がネットワーク トラフィックを認識するためには、ポート ミラーリングを構成する必要があります。 ポート ミラーリングは、トラフィックを 1 つのポート (コピー元ポート) から別のポート (コピー先ポート) にコピーします。

## Windows PowerShell スクリプトを使用したポート ミラーリングの検証

1. このスクリプトのテキストを ATAdiag.ps1 という名前のファイルに保存します。
2. このスクリプトを ATA ゲートウェイから実行します。
スクリプトが ATA ゲートウェイからドメイン コントローラーへの ICMP トラフィックを生成し、ドメイン コントローラー上のキャプチャ NIC でそのトラフィックを探します。
ATAゲートウェイが、ATA コンソールで入力されたドメイン コントローラーの IP アドレスと同じ宛先 IP アドレスの ICMP トラフィックを認識すると、ポート ミラーリングは構成されたと判断されます。 

スクリプト実行方法の例：

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## Net Mon を使用したポート ミラーリングの検証
1.  [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865)のインストール.

    > [!IMPORTANT]
    > ATA ゲートウェイには、Microsoft Message Analyzer やその他のトラフィック キャプチャ ソフトウェアをインストールしないでください。

2.  ネットワーク モニターを開き、新しいキャプチャ タブを作成します。

    1.  **キャプチャ** ネットワーク アダプター、またはポート ミラーリングの宛先として構成されているスイッチ ポートに接続されるネットワーク アダプターのみを選択します。

    2.  P-Mode が有効になっていることを確認します。

    3.  **[新しいキャプチャ]** をクリックします。.

        ![[新しいキャプチャの作成] タブの画像](media/ATA-Port-Mirroring-Capture.jpg)

3.  [表示フィルター] ウィンドウに「**KerberosV5 OR LDAP**」と入力し、**[適用]** をクリックします。.

    ![KerberosV5 or LDAP フィルター適用の画像](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  **[開始]** をクリックして、キャプチャ セッションを開始します。 ドメイン コントローラーとのトラフィックが表示されない場合は、ポート ミラーリングの構成を見直してください。

    ![キャプチャ セッション開始の画像](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > ドメイン コントローラーとのトラフィックが表示されることを必ず確認してください。
    

5.  どちらかの方向のトラフィックのみが表示される場合は、ネットワーキング チームまたは仮想化チームの協力を得てポート ミラーリングの構成をトラブルシューティングする必要があります。

## 参照

- [ポート ミラーリングの構成](configure-port-mirroring.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


