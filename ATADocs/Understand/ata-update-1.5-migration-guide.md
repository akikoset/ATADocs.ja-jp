---
# required metadata

title: ATA バージョン 1.5 移行ガイド |Microsoft Advanced Threat Analytics
description: ATA をバージョン 1.5 に更新する手順
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

# ATA バージョン 1.5 移行ガイド
ATA バージョン 1.5 では、次の機能が強化されています。

-   検出時間の短縮

-   NAT (ネットワーク アドレス変換) デバイスの自動検出アルゴリズムの強化

-   ドメイン不参加デバイスの名前解決プロセスの強化

-   製品更新時のデータ移行のサポート

-   何千ものエンティティが関係する不審なアクティビティに対する UI 応答時間の短縮

-   アラート監視の自動解決の強化

-   監視とトラブルシューティングを強化するためのパフォーマンス カウンターの追加

## ATA バージョン 1.5 への更新
> [!NOTE]
> お使いの環境にまだ ATA がインストールされていない場合は、バージョン 1.5 を含む ATA の完全なバージョンをダウンロードして、「[ATA のインストール](/advanced-threat-analytics/deploy-use/install-ata)」に記載されている標準的なインストール手順を実行します。.

既に ATA バージョン 1.4 をデプロイしている場合は、インストールを更新するために必要な手順を実行します。

次の手順に従って、ATA をバージョン 1.5 に更新してください。

1.  [バージョン 1.5 の更新プログラムをダウンロードする](http://aka.ms/ata1_5update)
      > [!NOTE]
         更新された ATA の完全バージョンを使用して、バージョン 1.5 に更新することもできます。


2.  ATA センターを更新する

3.  更新された ATA ゲートウェイ パッケージをダウンロードする

4.  ATA ゲートウェイを更新する

    > [!IMPORTANT]
    > ATA が正しく機能するよう、すべての ATA ゲートウェイを更新します。

### 手順 1: ATA センターを更新する

1.  データベースをバックアップします (省略可能)。

    -   ATA センターが仮想マシンとして実行されており、チェックポイントを取得する必要がある場合は、最初に仮想マシンをシャット ダウンします。

    -   ATA センターが物理サーバーで実行されている場合は、推奨される手順に従って [MongoDB をバックアップ](https://docs.mongodb.org/manual/core/backups/)します。.

2.  更新ファイル (Microsoft ATA センターの Update.exe) を実行し、画面の指示に従って更新プログラムをインストールします。

    1.  **[ようこそ]**ページで使用する言語を選択し、**[次へ]** をクリックします。.

    2.  使用許諾契約書を読み、条項に同意する場合はチェック ボックスをオンにして **[次へ]** をクリックします。.

    3.  完全な移行 (既定値) か部分的な移行のいずれかを選択します。

        ![完全な移行または部分的な移行を選択する](media/ATA-center-fullpartial.png)

        -   **部分的な**移行を選択した場合、ATA によって収集されたネットワーク トラフィックや分析された Windows イベント転送はすべて削除されます。また、ユーザーの動作プロファイルを再度学習する必要があり、これには少なくとも 3 週間かかります。 ディスクの容量が不足している場合は、**部分的な**移行が役立ちます。

        -   **完全な**移行を実行する場合は、追加のディスク容量が必要です (更新ページで計算されます)。また、ネットワーク トラフィックによっては移行時間が長くなることがあります。 完全な移行では、以前に収集されたすべてのデータとユーザーの動作プロファイルが保持されます。ATA で動作プロファイルを学習するための時間はかからず、更新後すぐに異常な動作を検出できます。

3.  **[更新]** をクリックします。 [更新] をクリックすると、更新手順が完了するまで ATA はオフラインになります。

4.  ATA センターが更新されると、ATA ゲートウェイが最新でないことが報告されます。

    ![ゲートウェイが最新でないことを示す画像](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - ATA が正しく機能するよう、すべての ATA ゲートウェイを更新します。

### 手順 2. ATA ゲートウェイ セットアップ パッケージをダウンロードする
ドメイン接続設定を構成した後、ATA ゲートウェイ セットアップ パッケージをダウンロードすることができます。

ATA ゲートウェイ パッケージをダウンロードするには:

1.  以前にダウンロードした古いバージョンの ATA ゲートウェイ パッケージがあれば削除します。

2.  ATA ゲートウェイ マシンでブラウザーを開き、ATA コンソールの ATA センターで構成した IP アドレスを入力します。 ATA コンソールが開いたら、設定アイコンをクリックして **[構成]** を選択します。.

    ![構成設定アイコン](media/ATA-config-icon.JPG)

3.  **[ATA ゲートウェイ]** タブで **[ATA ゲートウェイ セットアップのダウンロード]** をクリックします。.

4.  パッケージをローカルに保存します。

zip ファイルには次のものが含まれます。

-   ATA ゲートウェイ インストーラー

-   ATA センターへの接続に必要な情報が記載された構成設定ファイル

### 手順 3: ATA ゲートウェイを更新する

1.  各 ATA ゲートウェイで ATA ゲートウェイ パッケージからファイルを抽出し、Microsoft ATA ゲートウェイ セットアップ ファイルを実行します。

    > [!NOTE]
    > この ATA ゲートウェイ パッケージを使用して、新しい ATA ゲートウェイをインストールすることもできます。

2.  以前の設定は保持されますが、サービスが再開されるまでに数分かかる場合があります。

3.  デプロイされているすべての ATA ゲートウェイでこの手順を繰り返します。

> [!NOTE]
> ATA ゲートウェイが正常に更新されると、ATA ゲートウェイが最新でないことを示す通知は削除されます。

すべての ATA ゲートウェイから正常に同期されたことが報告され、更新された ATA ゲートウェイ パッケージが利用可能というメッセージが表示されなくなれば、すべての ATA ゲートウェイが正常に更新されています。

![更新されたゲートウェイの画像](media/ATA-gw-updated.png)

## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->

