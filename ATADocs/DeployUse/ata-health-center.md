---
# required metadata

title: ATA ヘルス センター | Microsoft Advanced Threat Analytics
description: ATA ヘルス センターを使用して ATA サービスの動作を確認し、問題が発生している可能性がある場合にアラートを受け取ることができます。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA ヘルス センター
ATA ヘルス センターでは、ATA サービスの動作を確認して、問題ある場合にアラートを受け取ることができます。

## ATA ヘルス センターを操作する
ATA ヘルス センターでは、メニュー バーのヘルス センター アイコンの上に警告 (赤色のドット) を表示することで、問題があることを知らせます。

![ATA ヘルス センターの赤色のドットのツールバー](media/ATA-Health-Center-Alert-red-dot.png)

### ATA の正常性を管理する
システムの全体的な正常性を確認するには、メニュー バーでヘルス センター アイコンをクリックします。 ![ATA ヘルス センター アイコン](media/ATA-red-dot.png)

-   オープン状態のアラートは、**[解決済み]** または **[無視]** に設定できます。 [アラート] で、**[オープン]** をクリックして **[解決済み]** または **[無視]** のいずれかにスクロールします。

-   問題を解決しても ATA でまだ解決していない問題として検出された場合、問題は自動的に **[オープン]** の問題一覧に戻されます。 オープン状態の問題が解決されたことが ATA で検出された場合、**[解決済み]** の問題一覧に移動されます。

-   **[無視]** の問題とは、ATA でのチェックが不要と判断した問題です。たとえば、存在は把握しているものの解決する予定がない問題や、今後通知を受け取らない問題として **[オープン]** の問題一覧に表示しない場合は、**[無視]** に設定します。

![ATA ヘルス センターの問題のイメージ](media/ATA-Health-Issue.JPG)

## 参照
- [ATA 検出設定の操作](working-with-detection-settings.md)
- [不審なアクティビティの処理](working-with-suspicious-activities.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


