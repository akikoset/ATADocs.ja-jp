---
# required metadata

title: ATA のインストール - 手順 2 | Microsoft Advanced Threat Analytics
description: ATA のインストールの手順 2 では、ATA センター サーバーでドメイン接続設定を構成します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 2

>[!div class="step-by-step"] [« 手順 1](install-ata-step1.md)
[手順 3 »](install-ata-step3.md)

## 手順 2. ATA ゲートウェイの全般的な設定の構成
**[全般]** 設定タブの設定は、ATA センターによって管理されるすべての ATA ゲートウェイに適用されます。

ATA ゲートウェイの全般的な設定を構成するには、次の手順を実行します:

1.  ATA コンソールを開いてログインします。 方法については、「[ATA コンソールの使用](working-with-ata-console.md)」を参照してください。

2.  設定アイコンをクリックして**[構成]** を選択します。

    ![ATA ゲートウェイの構成設定](media/ATA-config-icon.JPG)

3.  **[全般]** タブの**[ATA ゲートウェイ]**で次の情報を入力し、 **[保存]**をクリックします。

    |フィールド|コメント|
    |---------|------------|
    |**ユーザー名** (必須)|読み取り専用ユーザーの名前を入力します (例: **user1**)。|
    |**パスワード** (必須)|読み取り専用ユーザーのパスワードを入力します (例: **Pencil1**)。 **注:** このパスワードが正しいことを確認します。 間違ったパスワードを保存すると、ATA ゲートウェイ サーバーで実行されている ATA サービスは停止します。|
    |**ドメイン** (必須)|読み取り専用ユーザーのドメインを入力します (例: **contoso.com**)。 **注:** ユーザーが配置されているドメインの完全な FQDN を入力することが重要です。 たとえば、ユーザーのアカウントが corp.contoso.com というドメインにある場合は、contoso.com ではなく `corp.contoso.com` と入力する必要があります。|
    |すべての ATA ゲートウェイを自動更新する |この設定を有効にした場合、今後リリースされるバージョンで ATA センターを更新すると、すべての ATA ゲートウェイが自動的に更新されます。|

    ![ATA ドメイン接続設定の画像](media/ata-domain-connectivity-user.jpg)



>[!div class="step-by-step"] [« 手順 1](install-ata-step1.md)
[手順 3 »](install-ata-step3.md)


## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO3-->


