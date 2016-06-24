---
# required metadata

title: ATA 構成の変更 - IIS 証明書 | Microsoft Advanced Threat Analytics
description: IIS が ATA センター用に使用する証明書を変更する方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 構成の変更 - IIS 証明書

>[!div class="step-by-step"]
[« ATA コンソールの IP アドレス](modifying-ata-config-consoleip.md)
[ドメイン接続パスワード »](modifying-ata-config-dcpassword.md)

## IIS 証明書の変更
コンソールでは、ATA センター サービスの証明書を選択して変更できますが、IIS によって使用される証明書を変更することはできません。

これを変更するには、次の手順を実行します。

> [!NOTE]
> IIS 証明書を変更したら、新しい ATA ゲートウェイをインストールする前に、ATA ゲートウェイ セットアップ パッケージをダウンロードする必要があります。

ATA コンソール用に IIS によって使用される IP アドレスを変更する必要がある場合は、ATA センター サーバーから次の操作を実行します。

1.  ATA センター サーバーに新しい証明書をインストールします。

2.  インターネット インフォメーション サービス (IIS) マネージャーを開きます。

3.  サーバーの名前を展開し、**[サイト]** を展開します。.

4.  Microsoft ATA コンソールのサイトを選択し、[**Actions (アクション)**] ウィンドウで **[バインド]** をクリックします。.

    ![ATA コンソールのバインド操作](media/ATA-console-change-IP-bindings.jpg)

5.  **[HTTPS]** を選択し、**[編集]** をクリックします。.

6.  **[SSL 証明書]** で、新しい証明書を選択します。

7.  新しい ATA ゲートウェイをインストールする前に、ATA ゲートウェイ セットアップ パッケージをダウンロードします。

>[!div class="step-by-step"]
[« ATA コンソールの IP アドレス](modifying-ata-config-consoleip.md)
[ドメイン接続パスワード »](modifying-ata-config-dcpassword.md)

## 参照
- [ATA コンソールの使用](working-with-ata-console.md)
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


