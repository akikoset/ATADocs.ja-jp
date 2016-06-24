---
# required metadata

title: 製品利用統計情報の設定の管理 | Microsoft Advanced Threat Analytics
description: ATA によって収集されるデータ、およびデータ収集を無効にする手順を説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 製品利用統計情報の設定の管理
Advanced Threat Analytics (ATA) は、ATA に関する匿名化された利用統計情報データを収集し、HTTPS 接続経由でデータをマイクロソフト サーバーに転送します。  マイクロソフトはこのデータを ATA の今後のバージョンの向上に役立てます。

## 収集したデータ
収集した匿名データには、次の情報が含まれます：

-   ATA センターと ATA ゲートウェイの両方のパフォーマンス カウンター

-   ATA のライセンスのプロダクト ID

-   ATA センターの展開日

-   展開済みの ATA ゲートウェイの数

-   次の匿名化された Active Directory 情報:

    -   名前をアルファベット順に並べたときに最初に来るドメインのドメイン ID

    -   ドメイン コントローラーの数

    -   ポート ミラーリング経由で ATA によって監視されるドメイン コントローラーの数

    -   サイトの数

    -   コンピューターの台数

    -   グループの数

    -   ユーザーの数

-   疑わしいアクティビティ – 不審なアクティビティ検出のため次の匿名データが収集されます。

    (コンピューター名、ユーザー名、および IP アドレスは収集**されません**)

    -   疑わしいアクティビティの種類

    -   疑わしいアクティビティの ID

    -   状態

    -   開始時刻と終了時刻

    -   入力内容

### データ収集を無効にする
利用統計情報データの収集とマイクロソフトへの送信を停止するには、次の手順を実行します：

1.  ATA コンソールにログインし、ツールバーの 3 つのドットをクリックして、**[バージョン情報]** をクリックします。

2.  **[利用状況の情報をお送りいただき、今後のカスタマー エクスペリエンスの向上にご協力ください]** ボックスを選択解除します。

## 関連項目
- [バージョン 1.6 の新機能](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


