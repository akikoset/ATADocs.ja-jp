---
# required metadata

title: ATA 構成の変更 - ATA センターの IP アドレス | Microsoft Advanced Threat Analytics
description: ATA センターの IP アドレス、ポート、または証明書を変更する方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 構成の変更 - ATA センターの IP アドレス

>[!div class="step-by-step"]
[ATA センターの証明書 »](modifying-ata-config-centercert.md)

初期展開後の ATA センターの変更は、慎重に行う必要があります。 以下の手順に従って、IP アドレス、ポート、または証明書を更新できます。

## ATA センター サーバーで使用される IP アドレスの変更
ATA センターの IP アドレス、ポート、または証明書を変更する必要がある場合は、以下を考慮してください。

ATA ゲートウェイは、接続先の ATA センターの IP アドレスをローカルに格納します。 また、定期的 ATA センターに接続し、構成の変更をダウンロードします。 ATA ゲートウェイの ATA センターへの接続方法変更するには、次の 2 ステージのプロセスに従います。

-   第 1 ステージ – ATA センター サービスで使用する、ATA センター サービスの IP アドレスとポートを更新します。 この時点で、ATA センターはまだ元の IP アドレスをリッスンしており、ATA ゲートウェイがその構成を同期するときに、ゲートウェイは ATA センター用の 2 つの IP アドレスを所有します。 ATA ゲートウェイは元の (最初の) IP アドレスを使用して接続できる限り、新しい IP アドレスおよびポートの使用を試行しません。

-   第 2 ステージ – すべての ATA ゲートウェイが、更新された構成と同期されたら、ATA センターがリッスンする新しい IP アドレスとポートをアクティブ化します。 新しい IP アドレスをアクティブ化すると、ATA センター サービスが新しい IP アドレスにバインドされます。 ATA ゲートウェイは元のアドレスに接続できなくなり、ATA センター用の 2 つ目の (新しい) の IP アドレスで接続を試行します。 新しい IP アドレスで ATA センターに接続した後、ATA ゲートウェイは最新の構成をダウンロードし、ATA センター用の 1 つの IP アドレスを所有します。 (プロセスを再度開始していない限り。)

> [!NOTE]
> -   ATA ゲートウェイが第 1 ステージでオフラインであり、更新された構成を取得していない場合、ATA ゲートウェイ上の構成 JSON ファイルを手動で更新する必要があります。
> -   新しい IP アドレスが ATA センター サーバーにインストールされたら、変更を行うときに IP アドレスの一覧からそれを選択できます。 ただし、何らかの理由で ATA センター サーバーに IP アドレスをインストールできない場合、カスタム IP アドレスを選択し、それを手動で追加できます。 IP アドレスがサーバーにインストールされた後、新しい IP アドレスをアクティブ化できるようになります。
> -   新しい IP アドレスをアクティブ化した後、新しい ATA ゲートウェイを展開する必要がある場合は、ATA ゲートウェイ セットアップ パッケージを再度ダウンロードする必要があります。

1.  ATA コンソールを開きます。

2.  ツール バーの設定オプションを選択し、**[構成]** を選択します。.

    ![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

3.  **[全般]** を選択します。.

4.  **[ATA センター サービスの IP アドレス: ポート]** で、既存のいずれかの IP アドレスを選択するか、**[Add custom IP address (カスタム IP アドレスを追加)]** を選択して、IP アドレスを入力します。

5.  **[保存]** をクリックします。.

6.  何個の ATA ゲートウェイが最新の構成と同期されたかを示す通知が表示されます。

    ![ゲートウェイと同期された ATA センターのイメージ](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >新しい構成を有効にする前に、すべての ATA ゲートウェイが最新の構成と同期されていることを検証します。 すべての ATA ゲートウェイが同期する前に、新しい構成をアクティブ化すると、各 ATA ゲートウェイが予期したとおりに機能停止する可能性があります。 ATA ゲートウェイのいずれかが同期されていない場合は、[アクティブ化] をクリックすると、このエラーが表示されます。
    >
    >    ![ATA ゲートウェイ同期エラー](media/ataGW-not-synced.png)


7.  すべての ATA ゲートウェイが同期されたら、**[アクティブ化]** をクリックして、新しい IP アドレスをアクティブ化します。

    > [!NOTE]
    > カスタム IP アドレスを入力した場合、ATA センターに IP アドレスをインストールするまで **[アクティブ化]** をクリックすることはできません。

8.  変更がアクティブ化されたら、すべての ATA ゲートウェイでその構成を同期できることを確認します。 通知バーに、構成と正常に同期された ATA ゲートウェイの数が示されます。

>[!div class="step-by-step"]
[ATA センターの証明書を変更する »](modifying-ata-config-centercert.md)


## 参照
- [ATA コンソールの使用](working-with-ata-console.md)
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


