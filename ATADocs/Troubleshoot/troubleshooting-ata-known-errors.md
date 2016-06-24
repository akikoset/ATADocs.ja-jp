---
# required metadata

title: ATA エラー ログのトラブルシューティング | Microsoft Advanced Threat Analytics
description: ATA の一般的なエラーをトラブルシューティングする方法についての説明 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA エラー ログのトラブルシューティング
このセクションでは、ATA の展開で発生する可能性のあるエラーと、そうしたエラーを解決するために必要な手順について説明します。
## ATA ゲートウェイのエラー
|エラー|説明|解決策|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: ローカル エラーが発生しました|ATA ゲートウェイは、ドメイン コントローラーに対する認証に失敗しました。|1.DNS サーバーで、ドメイン コントローラーの DNS レコードが正しく構成されていることを確認します。 <br>2.ATA ゲートウェイの時刻がドメイン コントローラの時刻と同期されていることを確認します。|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Failed to validate certificate chain (証明書チェーンの検証に失敗しました)|ATA ゲートウェイは、ATA センターの証明書の検証に失敗しました。|1.ATA ゲートウェイで、信頼された証明機関の証明書ストアにルート証明機関証明書がインストールされていることを確認します。 <br>2.証明書失効リスト (CRL) が利用可能であり、証明書の失効の検証を実行できることを確認します。|
|Microsoft.Common.ExtendedException: Failed to parse time generated (生成された時間を解析できませんでした)|ATA ゲートウェイは、SIEM から転送された syslog メッセージを解析できませんでした。|SIEM が ATA でサポートされているいずれかの形式でメッセージを転送するように構成されていることを確認します。|
|System.ServiceModel.FaultException: メッセージのセキュリティを検証しているときにエラーが発生しました。|ATA ゲートウェイは、ATA センターに対する認証に失敗しました。|ATA ゲートウェイの時刻が ATA センターの時刻と同期されていることを確認してください。|
|System.ServiceModel.EndpointNotFoundException: net.tcp://center.ip.addr:443/IEntityReceiver に接続できませんでした|ATA ゲートウェイは、ATA センターへの接続を確立できませんでした。|ネットワーク設定が正しいこと、および ATA ゲートウェイと ATA センター間のネットワーク接続がアクティブであることを確認してください。|
|System.DirectoryServices.Protocols.LdapException: LDAP サーバーは使用できません。|ATA ゲートウェイは、LDAP プロトコルを使用してドメイン コントローラーにクエリを行うことができませんでした。|1. ATA が Active Directory ドメインへの接続に使用するユーザー アカウントに、Active Directory ツリーのすべてのオブジェクトに対する読み取りアクセス権があることを確認します。 <br>2. ATA の使用するユーザー アカウントからの LDAP クエリを禁止するようにドメイン コントローラーが設定されていないことを確認します。|
|Microsoft.Tri.Infrastructure.ContractException: Contract exception (契約の例外)|ATA ゲートウェイは、ATA センターと構成を同期できませんでした。|ATA コンソールで ATA ゲートウェイの構成を行ってください。|
|System.Reflection.ReflectionTypeLoadException: Unable to load one or more of the requested types (要求された型のうち 1 つまたは複数を読み込めませんでした)。 詳細については、LoaderExceptions プロパティを取得してください。|メッセージ アナライザーは、ATA ゲートウェイにインストールされます。| メッセージ アナライザーをアンインストールします。|
|Error [Layout] System.OutOfMemoryException: Exception of type 'System.OutOfMemoryException' was thrown ('System.OutOfMemoryException' の例外がスローされました)。|ATA ゲートウェイには、十分なメモリがありません。|ドメイン コントローラー上のメモリ容量を増やします。|
|Fail to start live consumer (ライブ コンシューマーを開始できませんでした) ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: The PEFNDIS event provider is not ready (PEFNDIS イベント プロバイダーの準備ができていません)|PEF (メッセージ アナライザー) が正しくインストールされていません。|回避策については、サポートにお問い合わせください。|
|Installation failed with error (エラーが発生してインストールに失敗しました): 0x80070652|コンピューターに保留中の他のインストールがあります。|他のインストールが完了するまで待ちます。必要に応じて、コンピューターを再起動します。|

## ATA コンソールのエラー
|エラー|説明|解決方法|
|-------------|----------|---------|
|HTTP エラー 500.19 – 内部サーバー エラー|IIS URL Rewrite モジュールを正常にインストールできませんでした。|IIS URL Rewrite モジュールをアンイストールし、インストールし直してください。<br>[IIS URL Rewrite モジュールのダウンロード](http://go.microsoft.com/fwlink/?LinkID=615137)|

## 展開のエラー
|エラー|説明|解決方法|
|-------------|----------|---------|
|.Net Framework 4.6.1 のインストールはエラー 0x800713ec で失敗しました|サーバーに .Net Framework 4.6.1 の前提条件がインストールされていません。 |ATA をインストールする前に、サーバーに Windows 更新プログラム [KB2919442](https://www.microsoft.com/en-us/download/details.aspx?id=42135) と [KB2919355](https://support.microsoft.com/en-us/kb/2919355) がインストールされていることを確認してください。|

![ATA .NET のインストール エラーの画像](media/netinstallerror.png)


## 関連項目
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [イベント コレクションの構成](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows イベント転送を構成する](/advanced-threat-analytics/deploy-use/configure-event-collection#ATA_event_WEF)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


