---
# required metadata

title: ATA のサイレント インストール | Microsoft Advanced Threat Analytics
description: ここでは、ATA をサイレント モードでインストールする方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA サイレント インストール
このトピックでは、ATA をサイレント モードでインストールする手順の詳細を紹介します。
## 必要条件

Microsoft ATA v1.6 には Microsoft .NET Framework 4.6.1 のフル インストールが必要です。 

ATA のインストールや更新を行うと、.Net Framework 4.6.1 が自動的に Microsoft ATA の展開の一部としてインストールされます。

> [!Note] .Net Framework 4.6.1 のインストールには、サーバーの再起動が必要になる場合があります。 ドメイン コント ローラーに ATA ゲートウェイをインストールする場合は、これらのドメイン コント ローラーに対するメンテナンス期間のスケジュール設定を検討してください。
ATA サイレント インストール方法を使用すると、インストーラーは (必要な場合) インストールの最後にサーバーを自動的に再起動するように構成されます。 インストールの一部としてサーバーの再起動が行われるのを避けるには、`-NoRestart` フラグを使用します。 `-NoRestart` フラグを使用していて、再起動がインストールの一部として求められる場合、インストーラーはサーバーが再起動されるまで一時停止します。 展開の進行状況を追跡するには、**%AppData%\Local\Temp** に配置されている ATA インストーラーのログを監視します。.


## ATA センターをインストールする

次のコマンドを実行して ATA センターをインストールします。

**構文**：

    “Microsoft ATA Center Setup.exe” [/quiet] [/NoRestart] [/Help] [--LicenseAccepted] [NetFrameworkCommandLineArguments=”/q”] [InstallationPath=“<InstallPath>”] [DatabaseDataPath= “<DBPath>”] [CenterIpAddress=<CenterIPAddress>] [CenterPort=<CenterPort>] [CenterCertificateThumbprint=“<CertThumbprint>”] 
    [ConsoleIpAddress=<ConsoleIPAddress>] [ConsoleCertificateThumbprint=”<CertThumbprint >”]
    
**インストールオプション**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないインストーラーを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|○|.Net Framework のインストールのパラメーターを指定します。 .Net Framework のサイレント インストールを強制する場合に設定する必要があります。|
|LicenseAccepted|--LicenseAccepted|○|ライセンスが読み取られ、承認されたことを示します。 サイレント インストールでは設定する必要があります。|

**インストール パラメーター**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|InstallationPath|InstallationPath=“<InstallPath>”|×|ATA バイナリのインストール パスを設定します。 既定のパスは、 C:\Program Files\Microsoft Advanced Threat Analytics\Center です。|
|DatabaseDataPath|DatabaseDataPath= “<DBPath>”|×|ATA データベースのデータ フォルダーのパスを設定します。 既定のパスは、C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data です。|
|CenterIpAddress|CenterIpAddress=<CenterIPAddress>|○|ATA センター サービスの IP アドレスを設定します。|
|CenterPort|CenterPort=<CenterPort>|○|ATA センター サービスのネットワーク ポートを設定します。|
|CenterCertificateThumbprint|CenterCertificateThumbprint=“<CertThumbprint>”|×|ATA センター サービスの証明書の拇印を設定します。 この証明書は、ATA センターと ATA ゲートウェイ間の通信のセキュリティ保護に使用されます。 この証明書が設定されていない場合、インストールによって自己署名証明書が生成されます。|
|ConsoleIpAddress|ConsoleIpAddress=<ConsoleIPAddress>|○|ATA コンソールの IP アドレスを設定します。|
|ConsoleCertificateThumbprint|ConsoleCertificateThumbprint=”<CertThumbprint >”|×|ATA コンソールの証明書の拇印を指定します。 この証明書は、ATA Web サイトの ID の検証に使用されます。この証明書が指定されていない場合、インストールによって自己署名証明書が生成されます。|

**例**：
既定のインストール パスと単一の IP アドレスで ATA センターをインストールする場合は、次のコマンドを使用します。

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments="/q" CenterIpAddress=192.168.0.10
    CenterPort=444 ConsoleIpAddress=192.168.0.10

既定のインストール パス、2 つの IP アドレス、およびユーザー定義の証明書の拇印で ATA センターをインストールする場合は、次のコマンドを使用します。

    “Microsoft ATA Center Setup.exe” /quiet --LicenseAccepted NetFrameworkCommandLineArguments ="/q" CenterIpAddress=192.168.0.10 CenterPort=443 CenterCertificateThumbprint= ‎"1E2079739F624148ABDF502BF9C799FCB8C7212F”
    ConsoleIpAddress=192.168.0.11  ConsoleCertificateThumbprint=”G9530253C976BFA9342FD1A716C0EC94207BFD5A”

## ATA センターを更新する

次のコマンドを実行して ATA センターを更新します。

**構文**：

    Microsoft ATA Center Setup.exe” [/quiet] [-NoRestart] /Help] [NetFrameworkCommandLineArguments=”/q”]


**インストールオプション**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないインストーラーを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|○|.Net Framework のインストールのパラメーターを指定します。 .Net Framework のサイレント インストールを強制する場合に設定する必要があります。|


ATA を更新すると、インストーラーによって、ATA が既にサーバーにインストールされていること、および更新のインストール オプションは必要ないことが自動的に検出されます。

**例**：
ATA センターをサイレント モードで更新します。 大規模な環境では、 ATA センターの更新に時間がかかることがあります。 更新の進行状況を追跡するには、ATA ログを監視します。

        “Microsoft ATA Center Setup.exe” /quiet NetFrameworkCommandLineArguments="/q"

## ATA センターをサイレント モードでアンインストールします。

ATA センターのサイレント アンインストールを実行するには、次のコマンドを使用します。
**構文**：

    Microsoft ATA Center Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
     [--DeleteExistingDatabaseData]

**インストールオプション**：

|名前|構文|サイレント アンインストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないアンインストーラーを実行します。|
|アンインストール|/uninstall|○|サーバーから ATA センターのサイレント アンインストールを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|

**インストール パラメーター**：

|名前|構文|サイレント アンインストールに必須|説明|
|-------------|----------|---------|---------|
|DeleteExistingDatabaseData|DeleteExistingDatabaseData|×|既存のデータベース内のすべてのファイルを削除します。|

**例**：
既存のデータベース データをすべて削除して、ATA センターをサイレント モードでサーバーからアンインストールするには、次のコマンドを使用します。


    “Microsoft ATA Center Setup.exe” /quiet /uninstall --DeleteExistingDatabaseData

## ATA ゲートウェイのサイレント インストール
次のコマンドを実行して ATA ゲートウェイをサイレント モードでインストールします。

**構文**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] [/Help] [NetFrameworkCommandLineArguments ="/q"] 
    [GatewayCertificateThumbprint=”<CertThumbprint >”] [ConsoleAccountName=”<AccountName>”] 
    [ConsoleAccountPassword=”<AccountPassword>”]

**インストールオプション**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないインストーラーを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|○|.Net Framework のインストールのパラメーターを指定します。 .Net Framework のサイレント インストールを強制する場合に設定する必要があります。|
|LicenseAccepted|--LicenseAccepted|○|ライセンスが読み取られ、承認されたことを示します。 サイレント インストールでは設定する必要があります。|

**インストール パラメーター**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|GatewayCertificateThumbprint|GatewayCertificateThumbprint=”<CertThumbprint >”|×|ATA センター サービスの証明書の拇印を設定します。 この証明書は、ATA センターと ATA ゲートウェイ間の通信のセキュリティ保護に使用されます。 この証明書が設定されていない場合、インストールによって自己署名証明書が生成されます。|
|ConsoleAccountName|ConsoleAccountName=”<AccountName>”|○|ATA センターへの ATA ゲートウェイの登録に使用されるユーザー アカウント (user@domain.com) の名前を設定します。|
|ConsoleAccountPassword|ConsoleAccountPassword=”<AccountPassword>”|○|ATA センターへの ATA ゲートウェイの登録に使用されるユーザー アカウント (user@domain.com) のパスワードを設定します。|

**例**：
ATA ゲートウェイをサイレント モードでインストールし、指定された資格情報で ATA センターに登録するには、次のコマンドを使用します。

    “Microsoft ATA Gateway Setup.exe” /quiet NetFrameworkCommandLineArguments="/q" 
    ConsoleAccountName=”user@contoso.com” ConsoleAccountPassword=“userpwd”
    

## ATA ゲートウェイを更新する

次のコマンドを実行して ATA ゲートウェイをサイレント モードで更新します。

**構文**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/NoRestart] /Help] [NetFrameworkCommandLineArguments="/q"]


**インストールオプション**：

|名前|構文|サイレント インストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないインストーラーを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|
|NetFrameworkCommandLineArguments="/q"|NetFrameworkCommandLineArguments="/q"|○|.Net Framework のインストールのパラメーターを指定します。 .Net Framework のサイレント インストールを強制する場合に設定する必要があります。|


**例**：
ATA ゲートウェイをサイレント モードで更新するには、次のコマンドを使用します。

        Microsoft ATA Gateway Setup.exe /quiet NetFrameworkCommandLineArguments="/q"

## ATA ゲートウェイをサイレント モードでアンインストールする

ATA ゲートウェイのサイレント アンインストールを実行するには、次のコマンドを使用します。
**構文**：

    Microsoft ATA Gateway Setup.exe [/quiet] [/Uninstall] [/NoRestart] [/Help]
    
**インストールオプション**：

|名前|構文|サイレント アンインストールに必須|説明|
|-------------|----------|---------|---------|
|Quiet|スイッチを|○|UI やプロンプトが表示されないアンインストーラーを実行します。|
|アンインストール|/uninstall|○|サーバーからの ATA ゲートウェイのサイレント アンインストールを実行します。|
|NoRestart|/norestart|×|再起動の試行を抑制します。 既定では、再起動の前に確認のメッセージが表示されます。|
|ヘルプ|/help|×|ヘルプおよびクイック リファレンスを提供します。 すべてのオプションと動作の一覧を含む、setup コマンドの正しい使用方法を表示します。|

**例**：
サーバーから ATA ゲートウェイをサイレント モードでアンインストールするには、次のコマンドを使用します。


    Microsoft ATA Gateway Setup.exe /quiet /uninstall
    









## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)

<!--HONumber=May16_HO1-->


