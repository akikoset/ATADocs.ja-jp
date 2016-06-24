---
# required metadata

title: ATA ログを使用した ATA のトラブルシューティング | Microsoft Advanced Threat Analytics
description: ATA ログを使用して問題をトラブルシューティングする方法を説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA ログを使用した ATA のトラブルシューティング
ATA ログを使用すると、特定の時間の ATA の各コンポーネントの動作を把握できます。

## ATA ゲートウェイのログ
このセクションでの ATA ゲートウェイに関する記述はすべて、ATA Lightweight Gateway にも該当します。 

ATA ゲートウェイのログは、**Logs** というサブフォルダーに配置されています。 既定のインストール場所として、**C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs** に配置されます。

ATA ゲートウェイには、次のログが用意されています。

-   **Microsoft.Tri.Gateway.log** – このログには、ATA ゲートウェイで発生したすべてのこと (解決、エラーを含む) が含まれます。 主に、すべての操作の全体的な状態を発生した時間順に取得するために使用します。

-   **Microsoft.Tri.Gateway-Resolution.log** – このログには、ATA ゲートウェイがトラフィックで認識しているエンティティの解決情報が含まれます。 主に、エンティティ解決の問題を調査するために使用します。

-   **Microsoft.Tri.Gateway-Errors.log** – このログには、ATA ゲートウェイが検出したエラーのみが含まれます。 主に、正常性チェックを実行し、特定の時間に関連付ける必要のある問題を調査するために使用します。

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – このログはすべての同類のエラーと例外をグループ化し、頻度を計測します。
    このファイルは初めは空で、ATA ゲートウェイ サービスを起動したとき、毎分更新されます。 主に、ATA ゲートウェイに新しいエラーまたは問題がないかを把握するために使用します。エラーがグループ化されるので、新しい種類のエラーまたは問題がないかどうかをより簡単に把握できます。

> [!NOTE]
> 最初の 3 つのログ ファイルの最大許容サイズは 50 MB です。 このサイズに達すると、新しいログ ファイルが開き、前のログ ファイルの名前が "&lt;元のファイル名&gt;-Archived-00000" に変更されます (数値は名前が変更されるたびに増加します)。

### ATA センターのログ
ATA センターのログは、**Logs** というサブフォルダーに配置されています。 既定のインストール場所として、**C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs** に配置されます。

ATA センターには、次のログが用意されています。

-   **Microsoft.Tri.Center.log** – このログには、ATA センターで発生したあらゆるもの (検出、エラーを含む) が含まれます。 主に、すべての操作の全体的な状態を発生した時間順に取得するために使用します。

-   **Microsoft.Tri.Center-Detection.log** – このログには、ATA センターの検出の詳細のみが含まれます。 主に、検出の問題を調査するために使用します。

-   **Microsoft.Tri.Center-Errors.log** – このログには、ATA センターが検出したエラーのみが含まれます。 主に、正常性チェックを実行し、特定の時間に関連付ける必要のある問題を調査するために使用します。

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – このログはすべての同類のエラーと例外をグループ化し、頻度を計測します。
    このファイルは初めは空で、ATA センター サービスを起動するたびに、分刻みで更新されます。 主に、ATA センターに新しいエラーまたは問題がないかを把握するために使用します。エラーがグループ化されるので、新しい種類のエラーまたは問題がないかどうかをより簡単に把握できます。

> [!NOTE]
> 最初の 3 つのログ ファイルの最大許容サイズは 50 MB です。 このサイズに達すると、新しいログ ファイルが開き、前のログ ファイルの名前が "&lt;元のファイル名&gt;-Archived-00000" に変更されます (数値は名前が変更されるたびに増加します)。

### ATA コンソールのログ
ATA コンソールのログ (管理 API ログ) は、**Logs** というサブフォルダーに配置されます。 既定のインストール場所として、**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Management\Logs** に配置されます。

ATA コンソールには、次のログが用意されています。

-   **w3wp.log** – このログには、管理プロセス (IIS) で発生したすべての事項が含まれます。


-   **w3wp-Errors.log** – このログには、管理プロセス (IIS) が検出したエラーのみが含まれます。


-   **8e75f9f1-ExceptionStatistics.log** – このログはすべての同類のエラーと例外をグループ化し、頻度を計測します。
    このファイルは初めは空で、ゲートウェイ サービスが起動するたびに、分刻みで更新されます。 主に、ATA センターに新しいエラーまたは問題がないかを把握するために使用します。エラーがグループ化されるので、新しい種類のエラーまたは問題がないかどうかをより簡単に把握できます。

> [!NOTE]
> 最初の 2 つのログ ファイルの最大許容サイズは 50 MB です。 このサイズに達すると、新しいログ ファイルが開き、前のログ ファイルの名前が "&lt;元のファイル名&gt;-Archived-00000" に変更されます (数値は名前が変更されるたびに増加します)。

### ATA 展開ログ
ATA 展開ログは、製品をインストールしたユーザーの一時ディレクトリに配置されます。 既定のインストール場所として、**C:\Users\Administrator\AppData\Local\Temp** (または %temp% の 1 つ上のディレクトリ) に配置されます。

ATA センターの展開ログ:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - このログは、ATA センターの展開プロセスの手順を示します。 主に、ATA センターの展開プロセスを追跡するために使用します。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - このログは、ATA センターの MongoDB 展開プロセスの手順を示します。 主に、MongoDB の展開プロセスを追跡するために使用します。

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - このログ ファイルは、ATA センター バイナリの展開プロセスの手順を示します。 主に、ATA センターのバイナリの展開を追跡するために使用します。

ATA ゲートウェイと ATA Lightweight Gateway の展開 ログ:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - このログは、ATA ゲートウェイの展開プロセスの手順を示します。 主に、ATA ゲートウェイの展開プロセスを追跡するために使用します。

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - このログ ファイルは、ATA ゲートウェイ バイナリの展開プロセスの手順を示します。 主に、ATA ゲートウェイ バイナリの展開を追跡するために使用します。

## 関連項目
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [イベント コレクションの構成](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows イベント転送を構成する](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


