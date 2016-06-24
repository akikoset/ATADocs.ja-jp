---
# required metadata

title: ATA データベースを使用した ATA のトラブル シューティング | Microsoft Advanced Threat Analytics
description: ATA データベースを使用して問題をトラブルシューティングする方法を説明します。 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA データベースを使用した ATA のトラブルシューティング
ATA は、そのデータベースとして MongoDB を使用します。
データベースを操作するには、既定のコマンドラインを使用するか、ユーザー インターフェイス ツールを使用して、高度なタスクやトラブルシューティングを実行できます。

## データベースとの対話
データベースを照会する既定の最も基本的な方法として、Mongo シェルを使用します。

1.  コマンドライン ウィンドウを開き、MongoDB bin フォルダーへのパスを変更します。 既定のパスは: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** です。

2.  `mongo.exe ATA` を実行します。 ATA をすべて大文字で入力してください。

|操作方法|構文|注|
|-------------|----------|---------|
|データベース内のコレクションを確認します。|`show collections`|エンド ツー エンド テストとして、トラフィックがデータベースに書き込まれていること、またイベント 4776 が ATA によって受信されていることを確認できます。|
|ユーザー ID など、ユーザー/コンピューター/グループ (UniqueEntity) の詳細を取得します。|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|特定の日に特定のコンピューターから送信された Kerberos 認証トラフィックを検索します。|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|&lt; ソース コンピューターの ID &gt; を取得するには、サンプルに示されているように UniqueEntity コレクションにクエリを実行します。<br /><br />Kerberos 認証など、各種のネットワーク アクティビティには、UTC 日付ごとに独自のコレクションがあります。|
|特定の日の特定のアカウントに関連付けられた特定のコンピューターから送信された NTLM トラフィックを検索します。|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|&lt; ソース コンピューターの ID &gt; と &lt; アカウントの ID &gt; を取得するには、サンプルに示されているように UniqueEntity コレクションにクエリを実行します。<br /><br />NTLM 認証など、各種のネットワーク アクティビティには、UTC 日付ごとに独自のコレクションがあります。|
|アカウントの有効日など、詳細プロパティを検索します。 |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|&lt; アカウントの ID&gt; を取得するには、サンプルに示されているように UniqueEntity コレクションにクエリを実行します。<br>アカウントがアクティブになっていた日付を表示するプロパティ名は "ActiveDates" と呼ばれます。 <br>
たとえば、異常な動作の機械学習アルゴリズムを実行させるために、アカウントに少なくとも 21 日間のアクティビティがあるかどうかを知りたい場合に使用します。|
|高度な構成を変更します。 この例では、すべての ATA ゲートウェイの送信キューのサイズを 10,000 に変更します。|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

次の例では、上に示した構文を使用したサンプル コードを提供します。 2015 年 10 月 20 日に発生した疑わしいアクティビティを調査し、この日に John Doe が実行した NTLM アクティビティに関する詳細を知りたいとします:<br /><br />最初に、John Doe の ID を検索します。

`db.UniqueEntity.find({Name: "John Doe"})`<br>"`_id`" の値として示されている John の ID を書き留めます。この例では、ID を "`123bdd24-b269-h6e1-9c72-7737as875351`" と仮定します。<br>次に、探している日付 (ここでは、2015 年 10 月 20 日) 以前の最も直近の日付のコレクションを検索します。<br>John Doe のアカウントの NTLM アクティビティを検索します。 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## ATA 構成ファイル
ATA の構成は、データベース内の "SystemProfile" コレクションに格納されます。
このコレクションは ATA センター サービスにより、SystemProfile.json というファイルに 1 時間おきにバックアップされます。 これは、"Backup" というサブフォルダーにあります。 既定の ATA インストール場所として、**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json** に配置されます。 

**注**: ATA に大幅な変更を加えるとき、このファイルをバックアップすることをお勧めします。

次のコマンドを実行して、すべての設定を復元できます。

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## 関連項目
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [イベント コレクションの構成](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows イベント転送を構成する](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


