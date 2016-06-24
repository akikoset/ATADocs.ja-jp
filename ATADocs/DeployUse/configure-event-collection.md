---
# required metadata

title: イベント コレクションの構成 | Microsoft Advanced Threat Analytics
description: ATA でのイベント コレクションを構成するためのオプションについて説明します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# イベント コレクションの構成
ATA では、検出機能の強化のために、Windows イベント ログ ID 4776 が必要になります。 これは、SIEM イベントをリッスンするように ATA ゲートウェイを構成するか、または [Windows イベント転送を構成](#configuring-windows-event-forwarding)することによって、ATA ゲートウェイに転送することができます。.

## イベント コレクション
ドメイン コントローラーとの間のネットワーク トラフィックの収集や分析に加え、ATA は Windows イベント 4776 を使用して ATA Pass-the-Hash 検出をさらに強化することができます。 これは、SIEM から、またはドメイン コントローラーから Windows イベント転送を設定することによって受信できます。 収集されたイベントは、ドメイン コントローラーのネットワーク トラフィック経由では利用できない追加情報を ATA に提供します。

### SIEM/Syslog
ATA が Syslog サーバーからデータを使用できるようにするには、以下の操作を行う必要があります。

-   ATA ゲートウェイ サーバーのいずれかを、SIEM/Syslog サーバーから転送されるイベントをリッスンして受理するように設定します。

-   ATA ゲートウェイに特定のイベントを転送するように SIEM/Syslog サーバーを構成します。

> [!IMPORTANT]
> -   すべての Syslog データを ATA ゲートウェイに転送しないでください。
> -   ATA は SIEM/Syslog サーバーからの UDP トラフィックをサポートします。

特定のイベントを別のサーバーに転送するように構成する方法については、SIEM/Syslog サーバーの製品ドキュメントを参照してください。 

### Windows イベント転送
SIEM/Syslog サーバーを使用しない場合は、ATA によって収集および分析される Windows イベント ID 4776 を転送するように Windows ドメイン コントローラーを構成することができます。 Windows イベント ID 4776 は NTLM 認証に関するデータを提供します。

## SIEM イベントをリッスンするように ATA ゲートウェイを構成する

1.  ATA ゲートウェイ構成で **Syslog リスナー UDP** を有効にします。.

    下の図に示すように、リスニング IP アドレスを設定します。 既定のポートは 514 です。

    ![Syslog リスナー UDP を有効にする画像](media/ATA-enable-siem-forward-events.png)

2.  Windows イベント ID 4776 を、上で選択した IP アドレスに転送するように SIEM または Syslog サーバーを構成します。 SIEM の構成の詳細については、各 SIEM サーバーの特定のフォーマット要件に関する SIEM オンライン ヘルプまたはテクニカル サポート オプションを参照してください。

### SIEM のサポート
ATA は、次の形式で SIEM イベントをサポートします。

#### RSA セキュリティ分析
&lt;Syslog ヘッダー&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   Syslog ヘッダーは省略可能です。

-   すべてのフィールドの間で "\n" という区切り文字が必要です。

-   フィールドの内容と順番は次のとおりです。

    1.  RsaSA 定数 (表示される必要があります)。

    2.  実際のイベントのタイムスタンプ (SIEM への到着時または ATA への送信時のタイムスタンプではないことを確認してください)。 可能であればミリ秒単位の精度にしてください。これは非常に重要です。

    3.  Windows イベント ID

    4.  Windows イベント プロバイダー名

    5.  Windows イベント ログ名

    6.  イベントを受信するコンピューターの名前 (この場合は DC)

    7.  ユーザー認証の名前

    8.  ソース ホストの名前

    9. NTLM の結果コード

-   上記の順番は重要であり、メッセージにはこれ以外の内容を含めることはできません。

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|ドメイン コントローラーがアカウントの資格情報の検証を試みました。|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   プロトコルの定義に準拠している必要があります。

-   Syslog ヘッダーなし。

-   (プロトコルに記載されているとおり) ヘッダー部分 (パイプで区切られた部分) が存在する必要があります。

-   _拡張_部分の次のキーは、イベント内に存在する必要があります。

    -   externalId = Windows イベント ID

    -   rt = 実際のイベントのタイムスタンプ (SIEM への到着時または弊社への送信時のタイムスタンプではないことを確認してください)。 可能であればミリ秒単位の精度にしてください。これは非常に重要です。

    -   cat = Windows イベント ログ名

    -   shost = ソース ホスト名

    -   dhost = イベントを受信するコンピューター (この場合は DC)

    -   duser = ユーザー認証

-   _拡張_部分の順番は重要ではありません。

-   これら 2 つのフィールドに対するカスタム キーと keyLable が存在する必要があります。

    -   “EventSource”

    -   “理由またはエラー コード” = NTLM の結果コード

#### Splunk
&lt;Syslog ヘッダー&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

コンピューターは、アカウントの資格情報の検証を試みました。

認証パッケージ:              MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

ログオン アカウント: 管理者

ソース ワークステーション:       SIEM

エラー コード:         0x0

-   Syslog ヘッダーは省略可能です。

-   すべての必須フィールドの間には “\r\n” という区切り文字があります。

-   フィールドは、キー=値の形式です。

-   次のキーは必ず存在し、値を持つ必要があります。

    -   EventCode = Windows イベント ID

    -   Logfile = Windows イベント ログ名

    -   SourceName = Windows イベント プロバイダー名

    -   TimeGenerated = 実際のイベントのタイムスタンプ (SIEM への到着時または ATA への送信時のタイムスタンプではないことを確認してください)。 形式は yyyyMMddHHmmss.FFFFFF (可能であればミリ秒単位の精度) に一致する必要があります。これは非常に重要です。

    -   ComputerName = ソース ホスト名

    -   Message = Windows イベントからの元のイベント テキスト

-   Message のキーと値は最後に来る必要があります。

-   キーと値のペアについて、順番は重要ではありません。

#### QRadar
QRadar を使用すると、エージェントでイベントを収集できるようになります。 エージェントを使用してデータを収集すると、時刻形式はミリ秒データを含めずに収集されます。 ATA ではミリ秒データが求められるため、エージェントレスの Windows イベント収集を使用するように QRadar を設定する必要があります。 詳細については、[http://www-01.ibm.com/support/docview.wss?uid=swg21700170] を参照してください。(http://www-01.ibm.com/support/docview.wss?uid=swg21700170 "QRadar: Agentless Windows Events Collection using the MSRPC Protocol (QRadar: MSRPC プロトコルを使用したエージェントレス Windows イベント収集)").

    <13>Feb 11 00:00:00 %IPADDRESS% AgentDevice=WindowsLog AgentLogFile=Security Source=Microsoft-Windows-Security-Auditing Computer=%FQDN% User= Domain= EventID=4776 EventIDCode=4776 EventType=8 EventCategory=14336 RecordNumber=1961417 TimeGenerated=1456144380009 TimeWritten=1456144380009 Message=The computer attempted to validate the credentials for an account. Authentication Package: MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 Logon Account: Administrator Source Workstation: HOSTNAME Error Code: 0x0

必要なフィールドは次のとおりです。

- 収集のエージェントの種類
- Windows イベント ログのプロバイダー名
- Windows イベント ログのソース
- DC の完全修飾ドメイン名
- Windows イベント ID

TimeGenerated は、実際のイベントのタイムスタンプです (SIEM への到着時または ATA への送信時のタイムスタンプではないことを確認してください)。 形式は yyyyMMddHHmmss.FFFFFF (可能であればミリ秒単位の精度) に一致する必要があります。これは非常に重要です。

Message は、Windows イベントの元のイベント テキストです。

各キーと値のペアの間に「\t」を挿入してください。

>[!NOTE] Windows イベントの収集で WinCollect を使用することはできません。

## Windows イベント転送を構成する
SIEM サーバーがない場合は、Windows イベント ID 4776 を ATA ゲートウェイのいずれかに直接転送するようにドメイン コントローラーを構成することができます。

1.  管理者特権を持つドメイン アカウントを使用して、すべてのドメイン コントローラーと ATA ゲートウェイ マシンにログオンします。
2. 接続しているすべてのドメイン コントローラーと ATA ゲートウェイが、同じドメインに参加していることを確認します。
3.  各ドメイン コントローラーで、管理者特権でのコマンド プロンプトから次のコマンドを入力します。
```
winrm quickconfig
```
4.  ATA ゲートウェイで、管理者特権でのコマンド プロンプトから次のコマンドを入力します。
```
wecutil qc
```
5.  各ドメイン コントローラーで、**[Active Directory ユーザーとコンピューター]** の **[Builtin]** フォルダーに移動して、**[Event Log Readers]** グループをダブルクリックします。<br>
![wef_ad_eventlogreaders](media/wef_ad_eventlogreaders.png)<br>
右クリックして **[プロパティ]** を選択します。 **[メンバー]** タブで、各 ATA ゲートウェイのコンピューター アカウントを追加します。
![wef_ad イベント ログ リーダーのポップアップ](media/wef_ad-event-log-reader-popup.png)
6.  ATA ゲートウェイで、イベント ビューアーを開いて **[サブスクリプション]** を右クリックし、**[サブスクリプションの作成]** を選択します。.  

    a. **[サブスクリプションの種類とソース コンピューター]** で **[コンピューターの選択]** をクリックし、ドメイン コントローラーを追加して接続をテストします。
    ![wef_subscription のプロパティ](media/wef_subscription-prop.png)

    b. **[収集するイベント]** で **[イベントの選択]** をクリックします。 **[ログ単位]** を選択して **[セキュリティ]** まで下にスクロールします。 次に、**[イベント ID を含める/除外する]** に「**4776**」と入力します。.<br>
    ![wef_4776](media/wef_4776.png)

    c. **[ユーザー アカウントを変更するか、詳細設定を構成する]** で **[詳細]** をクリックします。.
**[プロトコル]** を **[HTTP]** に設定し、**[ポート]** に「**5985**」と入力します。.<br>
    ![wef_http](media/wef_http.png)

7.  (省略可能) ポーリング間隔をより短くする場合は、ATA ゲートウェイでサブスクリプションのハートビートを 5 秒に設定してポーリング レートを速くします。
    wecutil ss <CollectionName>/cm:custom
    wecutil ss <CollectionName> /hi: 5000

8. ATA ゲートウェイの構成ページで、**[Windows イベント転送コレクション]** を有効にします。.

> [!NOTE]
この設定を有効にすると、ATA ゲートウェイはドメイン コントローラーから転送されていた Windows イベントの転送されたイベント ログを確認します。

詳細については、「[イベントを転送して収集するようにコンピューターを構成する](https://technet.microsoft.com/en-us/library/cc748890)」を参照してください。

## 参照
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


