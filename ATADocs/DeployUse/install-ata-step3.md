---
# required metadata

title: ATA のインストール - 手順 3 | Microsoft Advanced Threat Analytics
description: ATA のインストールの手順 3 では、ATA ゲートウェイ セットアップ パッケージをダウンロードします。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 3

>[!div class="step-by-step"]
[« 手順 2](install-ata-step2.md)
[手順 4 »](install-ata-step4.md)

## 手順 3. ATA ゲートウェイ セットアップ パッケージをダウンロードする
ドメイン接続設定を構成した後、ATA ゲートウェイ セットアップ パッケージをダウンロードすることができます。 ATA ゲートウェイは専用サーバーもしくはドメイン コントローラーにインストールすることができます。 ドメイン コントローラーにインストールする場合は、ATA 簡易ゲートウェイとしてインストールされます。 ATA 簡易ゲートウェイについての詳細は 「[ATA アーキテクチャ](/advanced-threat-analytics/plan-design/ata-architecture)」をご覧ください。. 

ATA ゲートウェイ パッケージをダウンロードするには:

1.  ATA コンソールで設定アイコンをクリックして、**[構成]** を選択します。.

    ![ATA ゲートウェイの構成設定](media/ATA-config-icon.JPG)

2.  **[ATA ゲートウェイ]** タブで **[ATA ゲートウェイ セットアップのダウンロード]** をクリックします。.

3.  パッケージをローカルに保存します。
4.  パッケージを、ATA ゲートウェイをインストールする専用サーバーまたはドメイン コントローラーにコピーします。 あるいは、専用サーバーまたはドメイン コントローラーから ATA コンソールを開くことで、この手順をスキップできます。

zip ファイルには次のものが含まれます。

-   ATA ゲートウェイ インストーラー

-   ATA センターへの接続に必要な情報が記載された構成設定ファイル


>[!div class="step-by-step"]
[« 手順 2](install-ata-step2.md)
[手順 4 »](install-ata-step4.md)

## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO1-->


