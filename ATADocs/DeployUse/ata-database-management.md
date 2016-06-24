---
# required metadata

title: ATA データベースの管理 | Microsoft Advanced Threat Analytics
description: ATA データベースの移動、バックアップ、復元をサポートする手順を紹介します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA データベース管理
ATA データベースを移動、バックアップ、復元する必要がある場合は、MongoDB の使用に関するこれらの手順を使用してください。

## ATA データベースをバックアップする
[関連する MongoDB のドキュメント](http://docs.mongodb.org/manual/administration/backup/)を参照する.

## ATA データベースを復元する
[関連する MongoDB のドキュメント](http://docs.mongodb.org/manual/administration/backup/)を参照する.

## ATA データベースを別のドライブに移動する

1.  **Microsoft Advanced Threat Analytics Center** サービスを停止します。

2.  **MongoDB** サービスを停止します。

3.  Mongo 構成ファイルを開きます。既定では C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg にあります。

    パラメーターを検索する `storage: dbPath`

4.  `dbPath` パラメーターに示すフォルダーを新しい場所に移動します。

5.  mongo 構成ファイル内の `dbPath` パラメーターを新しいフォルダー パスに変更し、ファイルを保存して閉じます。

    ![MongoDB の構成イメージを変更する](media/ATA-mongoDB-moveDB.png)

6.  **MongoDB** サービスを開始します。

7.  コマンド プロンプトを開き、　を実行して Mongo シェルを実行します。 `mongo.exe ATA` .

    既定では、mongo.exe は C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin にあります。

8.  次のコマンドを実行します： `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>` ここで&lt; New DB Location&gt; は新しいフォルダー パスです。

9.  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath を新しいフォルダー パスに更新します。

9. **Microsoft Advanced Threat Analytics Center** サービスを開始します。

## 参照
- [ATA アーキテクチャ](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


