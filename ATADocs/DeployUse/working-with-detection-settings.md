---
# required metadata

title: ATA 検出設定の操作 | Microsoft Advanced Threat Analytics
description: 特殊な状況にあるため、ネットワークの他のエンティティとは異なる処理をする必要がある IP アドレスとサブネットの一覧を構成する方法について説明します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 検出設定の操作
**検出**を構成するページで、特殊な状況にあるためにネットワークの他のエンティティとは多少異なる処理をする必要がある IP アドレスとサブネットの一覧を設定できます。

## 検出の設定
**[検出]** ページで、次の項目を定義できます。

-   **短期リース サブネット** - 組織に、IP アドレスが非常に短期であるサブネット (VPN IP アドレス サブネットや Wi-Fi サブネットなど) がある場合は、これらの IP アドレスとサブネットを ATA に入力することで、コンピューターと入力した範囲の IP アドレスの関連付けが他の IP アドレスよりも短い期間保存されることを ATA に通知することが重要です。

-   **ハニ―トークン アカウント SID** – これは、ネットワーク アクティビティがあってはならないユーザー アカウントです。 このアカウントは、ATA ハニートークン ユーザーとして構成されます。 誰かがこのユーザーアカウントを使おうとした場合、ATA は不審なアクティビティを作成し、悪意のあるアクティビティであることを示します。 ハニートークン ユーザーを構成するには、ユーザー名ではなく、ユーザー アカウントの SID が必要です。

IP アドレスは、次の検出から除外できます。 これらの一覧に IP アドレスを入力すると、ATA はその IP アドレスを指定された種類の検出アクティビティから除外します。

-   DNS 偵察から除外する IP アドレス

-   Pass-the-Ticket から除外する IP アドレス

## 参照
- [不審なアクティビティの処理](working-with-suspicious-activities.md)
- [ATA 構成の変更](modifying-ata-configuration.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


