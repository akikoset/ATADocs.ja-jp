---
# required metadata

title: ATA バージョン 1.6 移行ガイド | Microsoft Advanced Threat Analytics
description: ATA をバージョン 1.6 に更新する手順
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA バージョン 1.6 移行ガイド
ATA バージョン 1.6 では、次の機能が強化されています。

-   検出対象の新規追加

-   既存の検出機能の強化

-   ATA Lightweight Gateway

-   自動更新

-   ATA センターのパフォーマンスの改善

-   ストレージ要件の緩和

-   IBM QRadar のサポート

## ATA バージョン 1.6 への更新
> [!NOTE] 使用している環境にまだ ATA がインストールされていない場合は、バージョン 1.6 を含む ATA の完全なバージョンをダウンロードして、[ATA のインストール](/advanced-threat-analytics/deploy-use/install-ata) に記載されている標準的なインストール手順を実行します。

すでに ATA バージョン 1.5 を展開している場合は、展開を更新するために必要な手順を実行します。

> [!NOTE] ATA バージョン 1.4 に直接 ATA バージョン 1.6 をインストールすることはできません。 まず、ATA バージョン 1.5 をインストールする必要があります。 ATA 1.5 をインストールしないで、誤って ATA 1.6 をインストールしようとした場合、**新しいバージョンが既にコンピューターにインストールされています**というエラーが示されます。 ATA バージョン 1.5 をインストールする前に、(インストールが失敗した場合でも) コンピューター上に残された ATA 1.6 をアンインストールする必要があります。

次の手順に従って、ATA をバージョン 1.6 に更新してください。

1. アップグレード プロセスを開始する前に、[ATA バージョン 1.6 の更新時の移行エラー](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5) を処理するための手順を実行します。
2. アップグレードを完了するために、必要な空き領域があることを確認してください。 必要な空き領域の見積もりを取得する準備チェックに応じて、インストールを実行できます。その後、必要なディスク領域を割り当てた後に、アップグレードを再開できます。 アップグレード プログラムでは、データベース サイズの少なくとも 2% を使用します。詳しくは、「[ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)」をご覧ください。
1.  [バージョン 1.6 の更新プログラムをダウンロードする](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
このバージョンでは、ATA の新規展開と既存の展開の更新に同じインストール ファイル (Microsoft ATA Center Setup.exe) を使用します。

2.  ATA センターを更新する

3.  更新された ATA ゲートウェイ パッケージをダウンロードする

4.  ATA ゲートウェイを更新する

    > [!IMPORTANT] ATA が正しく機能するように、すべての ATA ゲートウェイを更新します。

### 手順 1: ATA センターを更新する

1.  データベースをバックアップします (省略可能)。

    -   ATA センターが仮想マシンとして実行されており、チェックポイントを取得する必要がある場合は、最初に仮想マシンをシャット ダウンします。

    -   ATA センターが物理サーバーで実行されている場合は、推奨される手順に従って [MongoDB をバックアップ](https://docs.mongodb.org/manual/core/backups/)します。

2.  インストール ファイル (Microsoft ATA Center Setup.exe) を実行し、画面の手順に従って更新プログラムをインストールします。

    1.  ATA 1.6 では .Net Framework 4.6.1 がインストールされている必要があります。 .Net Framework 4.6.1 がまだインストールされていない場合、ATA のインストールの一環としてインストールされます。<br>
    > [!NOTE].Net Framework 4.6.1 をインストールすると、サーバーの再起動が必要になる場合があります。 サーバーが再起動されるのを待ってから、ATA のインストールが続行されます。
5.  **ようこそ**ページで使用する言語を選択し、**[次へ]** をクリックします。

    6.  使用許諾契約書を読み、条項に同意する場合は **[次へ]** をクリックします。

    7.  これで、Microsoft Update を使用して、ATA を最新の状態にできるようになりました。  Microsoft Update のページで、**[Microsoft Update を使用して更新プログラムを確認する (推奨)]** を選択します。
    ![ATA の更新画像 ](media/ata_ms_update.png) これで、次に示すように、他の Microsoft 製品 (ATA を含む) の更新を有効化できるように、Windows の設定が変更されます。 
     ![Windows 自動更新の画像](media/ata_installupdatesautomatically.png)

    8.  インストールの開始前に、ATA により準備チェックが行われます。 チェック結果をレビューして、前提条件が正常に構成されていること、およびディスク領域に最小容量以上の空きがあることを確認してください。 
    ![ATA の準備チェックの画像](media/ata_install_readinesschecks.png)

    3.  **[更新]** をクリックします。 [更新] をクリックすると、更新手順が完了するまで ATA はオフラインになります。

4.  ATA センターが更新されると、ATA ゲートウェイが最新でないことが報告されます。

    ![ゲートウェイが最新でないことを示す画像](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - ATA が正しく機能するよう、すべての ATA ゲートウェイを更新します。

### 手順 2. ATA ゲートウェイ セットアップ パッケージをダウンロードする
ドメイン接続設定を構成すると、ATA ゲートウェイ セットアップ パッケージをダウンロードできるようになります。

ATA ゲートウェイ パッケージをダウンロードするには:

1.  以前にダウンロードした古いバージョンの ATA ゲートウェイ パッケージがあれば削除します。

2.  ATA ゲートウェイ マシンでブラウザーを開き、ATA コンソールの ATA センターで構成した IP アドレスを入力します。 ATA コンソールが開いたら、設定アイコンをクリックして **[構成]** を選択します。

    ![構成設定アイコン](media/ATA-config-icon.JPG)

3.  **[ATA ゲートウェイ]** タブで **[ATA ゲートウェイ セットアップのダウンロード]** をクリックします。

4.  パッケージをローカルに保存します。

zip ファイルには次のものが含まれます。

-   ATA ゲートウェイ インストーラー

-   ATA センターへの接続に必要な情報が記載された構成設定ファイル

### 手順 3: ATA ゲートウェイを更新する

1.  各 ATA ゲートウェイで ATA ゲートウェイ パッケージからファイルを抽出し、**Microsoft ATA Gateway Setup.exe** ファイルを実行します。

    > [!NOTE] この ATA ゲートウェイ パッケージを使用して、新しい ATA ゲートウェイをインストールすることもできます。

2.  以前の設定は保持されますが、サービスの再開に数分かかる場合があります。

3.  デプロイされているすべての ATA ゲートウェイでこの手順を繰り返します。

> [!NOTE] ATA ゲートウェイが正常に更新されると、特定の ATA ゲートウェイが最新でないことを示す通知は解消されます。

すべての ATA ゲートウェイから正常に同期されたことが報告され、更新された ATA ゲートウェイ パッケージが利用可能というメッセージが表示されなくなれば、すべての ATA ゲートウェイが正常に更新されています。

![更新されたゲートウェイの画像](media/ATA-gw-updated.png)


## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


