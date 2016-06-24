---
# required metadata

title: ATA バージョン 1.6 の新機能 | Microsoft Advanced Threat Analytics
description: ATA バージョン 1.6 の新機能と既知の問題を示します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA バージョン 1.6 の新機能
このリリース ノートは、Advanced Threat Analytics のバージョン 1.5 の既知の問題に関する情報を提供します。

## ATA 1.6 への更新での新機能
ATA バージョン 1.6 では、次の機能が強化されています。

-   検出対象の新規追加

-   既存の検出機能の強化

-   ATA Lightweight Gateway

-   自動更新

-   ATA センターのパフォーマンスの改善

-   ストレージ要件の緩和

-   IBM QRadar のサポート

### 検出対象の新規追加


- **悪意のある、データ保護に関する秘密情報の要求** データ保護 API (DPAPI) は、パスワード ベースのデータ保護サービスです。 この保護サービスは、ユーザーの機密情報 (Web サイトのパスワードやファイル共有の資格情報など) を格納するさまざまなアプリケーションで使用されています。 パスワードが失われるシナリオをサポートするため、ユーザーは、自分のパスワードが含まれない回復キーを使用して、保護されたデータを暗号化解除できます。 ドメイン環境では、攻撃者がリモートで回復キーを盗み、そのキーを使用して、ドメインに参加しているすべてのコンピューター内の保護されたデータを復号化する可能性があります。


- **Net Session による列挙** 偵察は、高度な攻撃 Kill Chain 内の主要な段階です。 ドメイン コントローラー (DC) は、サーバー メッセージ ブロック (SMB) プロトコルを使用してグループ ポリシー オブジェクトを配布するためのファイル サーバーとして機能します。 偵察フェーズの一環として、攻撃者が DC に対して、サーバー上のすべてのアクティブな SMB セッションを照会する可能性があります。これにより、攻撃者はその SMB セッションに関連付けられているすべてのユーザーおよび IP アドレスにアクセスできるようになります。 機密アカウントをターゲットにする場合、攻撃者が SMB セッションの列挙を使用する可能性があります。これにより、攻撃者はネットワークで水平方向の活動を行うことができるようになります。


- **悪意のあるレプリケーション要求** Active Directory 環境では、レプリケーションがドメイン コントローラー間で定期的に発生します。 攻撃者は、より侵入的なボリューム シャドウ コピーのような手法を使用せずに、Active Directory に格納されているデータ (パスワード ハッシュを含む) を取得できるように、Active Directory のレプリケーション要求をスプーフィング (ドメイン コントローラーに偽装する場合もあります) する可能性があります。


- **MS11-013 脆弱性の検出** Kerberos には、Kerberos サービス チケットの特定の要素を偽造できるという、権限昇格の脆弱性が存在します。 この脆弱性の悪用に成功した、悪意のあるユーザーまたは攻撃者は、昇格した特権によりドメイン コントローラーでトークンを取得する可能性があります。


- **異常なプロトコルの実装** (Kerberos または NTLM) 認証要求は通常、メソッドおよびプロトコルの標準セットを使用して実行されます。 ただし、認証の成功のために要求が満たす必要があるのは、特定の一連の要件のみです。 攻撃者は、これらのプロトコルを、環境内の標準の実装から少しの偏差で実装する可能性があります。 この偏差は、Pass-The-Hash、ブルート フォースなどの攻撃を実行しようとしている攻撃者の存在を示している可能性があります。


### 既存の検出機能の強化
ATA 1.6 には、ゴールデン チケット、ハニー トークン、ブルート フォース、リモート実行などの既存の検出機能での偽陽性および偽陰性のシナリオを減少させる、強化された検出ロジックが含まれています。

### ATA Lightweight Gateway
このバージョンの ATA では、ATA ゲートウェイの新しい展開オプションが導入されています。これにより、ATA ゲートウェイをドメイン コントローラーに直接インストールできます。 この展開 オプションでは、ATA ゲートウェイの重要でない機能が削除されています。また、DC で使用可能なリソースに基づく動的なリソース管理が導入され、DC の既存の操作に影響しないようにしています。 ATA Lightweight Gateway により、ATA 展開のコストが削減されます。 同時に、ハードウェア リソース容量が限られているか、またはポート ミラーリングのサポートをセットアップできないブランチ サイトでの展開が容易になります。
ATA Lightweight Gateway の詳細については 「[ATA architecture (ATA アーキテクチャ)](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway)」をご覧ください。

展開に関する考慮事項と、適切な種類のゲートウェイの選択に関する詳細については、「[ATA capacity planning (ATA 容量計画)](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)」をご覧ください。


### 自動更新
バージョン 1.6 以降では、Microsoft Update を使用して ATA センターを更新できます。 さらに、ATA ゲートウェイは、ATA センターへの標準的な通信チャネルを使用した自動更新が可能になりました。
### ATA センターのパフォーマンスの改善
このバージョンでは、データベースの負荷が軽くなり、すべての検出を実行する方法がより効率的になったことで、単一の ATA センターでさらに多くのドメイン コントローラーを監視できるようになりました。

### ストレージ要件の緩和
ATA 1.6 では、ATA データベースの実行に必要なストレージ領域が大幅に減少しました。この領域は、以前のバージョンで使用していた領域の 20% にすぎません。

### IBM QRadar のサポート
ATA は、以前からサポートされている SIEM ソリューションに加え、IBM の QRadar SIEM ソリューションからイベントを受け取れるようになりました。

## 既知の問題
このバージョンには、以下の既知の問題があります。

### 手動で移動したデータベースの新しいパスの認識に失敗する

データベース パスが手動で移動されている展開では、ATA 展開は、更新でデータベースの新しいパスを使用しません。 これにより、次の問題が発生する可能性があります。


- ATA は、古いネットワーク アクティビティを循環的に削除せずに、ATA センターのシステム ドライブの空き領域すべてを使用する可能性があります。


- ATA をバージョン 1.6 に更新するとき、次の図に示すように、更新前の準備チェックに失敗します。
    ![失敗した準備チェック](media/ata_failed_readinesschecks.png)
    >[!Important]
ATA をバージョン 1.6 にアップグレードする前に、次のレジストリ キーをデータベースの正しいパスで更新します。  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### ATA 1.5 から更新するとき、移行に失敗する
ATA 1.6 にアップグレードするときに、次のエラー コードが表示されて更新プロセスが失敗することがあります。

![ATA 1.6 への更新でのエラー](http://i.imgur.com/QrLSApr.png) このエラーが発生した場合は、**C:\Users\<ユーザー>\AppData\Local\Temp** にある展開ログを確認し、次の例外を探します。

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

次のエラーが表示される場合もあります。System.ArgumentNullException: 値は NULL にすることはできません。
    
これらのエラーのいずれかが表示された場合は、次の回避策を実行します。

**回避策**: 

1.  "data_old" フォルダーを一次フォルダー (通常は %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin にあります) に移動します。
2.  ATA センター バージョン 1.5 をアンインストールし、データベースのデータをすべて削除します。
![ATA 1.5 のアンインストール](http://i.imgur.com/x4nJycx.png)
3.  ATA センター バージョン 1.5 を再インストールします。 必ず、ATA 1.5 の以前のインストールと同じ構成を使用してください (証明書、IP アドレス、データベースのパスなど)。
4.  次のサービスを次の順序で停止します。
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  MongoDB データベース ファイルを "data_old" フォルダー内のファイルで置き換えます。
6.  次のサービスを次の順序で開始します。
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  ログを調べ、製品がエラーなしで実行されていることを確認します。
8.  "RemoveDuplicateProfiles.exe" ツールを [ダウンロード](http://aka.ms/ataremoveduplicateprofiles "ダウンロード")してメインのインストール パス (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center) にコピーします。
9.  管理者特権のコマンド プロンプトで "RemoveDuplicateProfiles.exe" を実行し、正常に完了するまで待ちます。
10. …\Microsoft Advanced Threat Analytics\Center\MongoDB\bin ディレクトリで **Mongo ATA** を実行し、次のコマンドを入力します。

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![回避策の更新](http://i.imgur.com/Nj99X2f.png)

これにより、WriteResult({ "nRemoved" : XX }) が返されます。“XX” は削除された不審なアクティビティの数です。 数値が 0 より大きければ、コマンド プロンプトを終了し、更新プロセスを続けます。


### Net Framework 4.6.1 が原因でサーバーの再起動が必要になる

.Net Framework 4.6.1 をインストールすると、サーバーの再起動が必要になる場合があります。 **Microsoft Advanced Threat Analytics Center セットアップ** ダイアログで [OK] をクリックをすると、サーバーは自動的に再起動されます。 これは、インストール前にメンテナンス期間を計画する必要があるため、ATA Lightweight Gateway をドメイン コントローラーにインストールする場合に特に重要です。
    ![.Net Framework が原因である再起動](media/ata-net-framework-restart.png)

### ネットワーク アクティビティの履歴が移行されなくなった
このバージョンの ATA では、検出エンジンが強化されています。このエンジンによって検出がさらに正確となり、偽陽性シナリオ (特に Pass-the-Hash) が大幅に減少しました。
新しい強化された検出エンジンでは、インライン検出テクノロジを利用することで、ネットワーク アクティビティの履歴にアクセスしなくても検出が可能になり、ATA センターのパフォーマンスが大幅に向上しました。 つまり、更新処理中のネットワーク アクティビティの履歴を移行する必要もありません。
ATA の更新手順では、調査のため将来必要になる場合に備えて、データが JSON ファイルとして `<Center Installation Path>\Migration` にエクスポートされます。

## 関連項目
[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

[ATA バージョン 1.6 移行ガイド](ata-update-1.6-migration-guide.md)

<!--HONumber=May16_HO4-->


