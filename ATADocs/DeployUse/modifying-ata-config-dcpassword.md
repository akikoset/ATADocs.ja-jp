---
# required metadata

title: ATA 構成の変更 - ドメイン接続パスワード | Microsoft Advanced Threat Analytics
description: ATA ゲートウェイのドメイン接続パスワードを変更する方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 構成の変更 - ドメイン接続パスワード

>[!div class="step-by-step"]
[« IIS 証明書](modifying-ata-config-iiscert.md)


## ドメイン接続パスワードの変更
ドメイン接続パスワードを変更する場合、入力したパスワードが正しいことを確認します。 正しくないと、ATA ゲートウェイ サービスの ATA ゲートウェイでの実行が停止されます。

これが発生したと思われる場合は、ATA ゲートウェイで、以下について Microsoft.Tri.Gateway-Errors.log ファイルを確認します。
`The supplied credential is invalid.`

これを修正するには、次の手順に従って ATA ゲートウェイのドメイン接続パスワードを更新します。

1.  ATA ゲートウェイ上の ATA コンソールを開きます。

2.  ツール バーの設定オプションを選択し、**[構成]** を選択します。.

    ![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

3.  **[全般]** を選択します。.

    ![ATAA ゲートウェイのパスワードの変更イメージ](media/ATA-GW-change-DC-password.JPG)

4.   **[全般]** で、パスワードを変更します。

5.  **[保存]** をクリックします。.

6.  パスワードを変更したら、ATA ゲートウェイ サービスが ATA ゲートウェイ サーバーで実行されていることを手動で確認します。

>[!div class="step-by-step"]
[« IIS 証明書](modifying-ata-config-iiscert.md)

## 関連項目
- [ATA コンソールの使用](working-with-ata-console.md)
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


