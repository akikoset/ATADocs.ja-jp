---
# required metadata

title: ATA 構成の変更 - ATA センターの証明書 | Microsoft Advanced Threat Analytics
description: ATA センター サーバー上のローカル コンピューター ストアの証明書を更新または置き換える 2 段階のプロセスについて説明します。 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 構成の変更 - ATA センターの証明書

>[!div class="step-by-step"]
[« ATA センター サーバーの IP アドレス](modifying-ata-config-centerip.md)
[ATA コンソールの IP アドレス »](modifying-ata-config-consoleip.md)

## ATA センターの証明書を変更する
証明書の期限が切れ、ATA センター サーバー上のローカル コンピューター ストアに新しい証明書をインストールして、証明書を更新または置き換える必要がある場合は、次の 2 ステージのプロセスに従って証明書を置き換えます。

-   第 1 ステージ – ATA センター サービスで使用する証明書を更新します。 この時点で、ATA センター サービスはまだ元の証明書にバインドされています。 ATA ゲートウェイでその構成が同期されるとき、相互認証用に 2 つの証明書が有効になります。 ATA ゲートウェイは元の証明書を使用して接続できる限り、新しい証明書の使用を試行しません。

-   第 2 ステージ – すべての ATA ゲートウェイが、更新された構成と同期されたら、ATA センター サービスにバインドされた新しい証明書をアクティブ化できます。 新しい証明書をアクティブ化すると、ATA センター サービスが証明書にバインドされます。 ATA ゲートウェイは ATA センター サービスを適切に相互に認証できないため、2 つ目の証明書を認証しようとします。 ATA センター サービスに接続した後、ATA ゲートウェイは最新の構成をダウンロードし、ATA センター用の 1 つの証明書を所有します。 (プロセスを再度開始していない限り。)

> [!NOTE]
> -   ATA ゲートウェイが第 1 ステージでオフラインであり、更新された構成を取得していない場合、ATA ゲートウェイ上の構成 JSON ファイルを手動で更新する必要があります。
> -   使用する証明書は、ATA ゲートウェイで信頼されている必要があります。
> -   新しい証明書をアクティブ化した後、新しい ATA ゲートウェイを展開する必要がある場合は、ATA ゲートウェイ セットアップ パッケージを再度ダウンロードする必要があります。

1.  ATA コンソールを開きます。

2.  ツール バーの設定オプションを選択し、**[構成]** を選択します。.

    ![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

3.  **[ATA センター]** を選択します。.

4.  **[証明書]** で、一覧からいずれかの証明書を選択します。

5.  **[保存]** をクリックします。.

6.  何個の ATA ゲートウェイが最新の構成と同期されたかを示す通知が表示されます。

7.  すべての ATA ゲートウェイが同期されたら、**[アクティブ化]** をクリックして、新しい証明書をアクティブ化します。
    >[!IMPORTANT]
    >新しい構成を有効にする前に、すべての ATA ゲートウェイが最新の構成と同期されていることを検証します。 すべての ATA ゲートウェイが同期する前に、新しい構成をアクティブ化すると、各 ATA ゲートウェイが予期したとおりに機能停止する可能性があります。 ATA ゲートウェイのいずれかが同期されていない場合は、[アクティブ化] をクリックすると、このエラーが表示されます。
    >
    >    ![ATA ゲートウェイ同期エラー](media/ataGW-not-synced.png)

8.  変更がアクティブ化されたら、すべての ATA ゲートウェイでその構成を同期できることを確認します。

>[!div class="step-by-step"]
[« ATA センター サーバーの IP アドレス](modifying-ata-config-centerip.md)
[ATA コンソールの IP アドレス »](modifying-ata-config-consoleip.md)

## 参照
- [ATA コンソールの使用](working-with-ata-console.md)
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


