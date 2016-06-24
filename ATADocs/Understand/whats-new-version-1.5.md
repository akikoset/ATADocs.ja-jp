---
# required metadata

title: ATA バージョン 1.5 の新機能 | Microsoft Advanced Threat Analytics
description: ATA バージョン 1.5 の新機能と既知の問題を示します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA バージョン 1.5 の新機能
このリリース ノートは、Advanced Threat Analytics のバージョン 1.5 の既知の問題に関する情報を提供します。

## ATA 1.5 への更新での新機能
ATA バージョン 1.5 では、次の機能が強化されています。

-   検出時間の短縮

-   NAT (ネットワーク アドレス変換) デバイスの自動検出アルゴリズムの強化

-   ドメイン不参加デバイスの名前解決プロセスの強化

-   製品更新時のデータ移行のサポート

-   何千ものエンティティが関係する不審なアクティビティに対する UI 応答時間の短縮

-   アラート監視の自動解決の強化

-   監視とトラブルシューティングを強化するためのパフォーマンス カウンターの追加

## 既知の問題
このバージョンには、以下の既知の問題があります。

### 新しい ATA ゲートウェイのインストールが失敗する
ATA 展開をバージョン 1.5 に更新した後、新しい ATA ゲートウェイをインストールすると、次のエラーが発生します: Microsoft Advanced Threat Analytics ゲートウェイがインストールされていません 

![ATA GW エラー](media/ata-install-error.png)

<b>対応策:</b><ataeval@microsoft.com> にメールを送信して、対応手順の指示を求めてください。
### 展開
"データベースのデータ パス" と "データベース ジャーナルパス" に指定したフォルダーは (ファイルもサブフォルダーもない) 空のフォルダーである必要があります。
空でない場合、デプロイは先に進みません。

### Zip ファイルからのインストール
ATA ゲートウェイをインストールするときは、zip ファイルからローカル ディレクトリにファイルを抽出し、そこからインストールしてください。 zip ファイルから直接 ATA ゲートウェイをインストールしないでください。直接実行すると、インストールは失敗します。

### 構成
ATA ゲートウェイの構成を設定した後、ATA ゲートウェイを初めて起動すると、サービスが完全に開始されるまで、「同期されていません」というラベルが表示されます。サービスの初回の開始は最大 10 分かかる場合があります。

### ネットワーク キャプチャ ソフトウェア
ATA ゲートウェイにインストールできる唯一のサポートされているネットワーク キャプチャ ソフトウェアは [Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865) です。 Microsoft Message Analyzer またはその他のネットワーク キャプチャ ソフトウェアをインストールしないでください。 その他のソフトウェアをインストールすると、ATA ゲートウェイが正しく機能しなくなります。

### 仮想化ホスト上の KB
仮想化ホスト上に KB 3047154 をインストールしないでください。 ポート ミラーリングが正常に動作しなくなる可能性があります。

## 関連項目

[ATA バージョン 1.5 移行ガイド](ata-update-1.5-migration-guide.md)

[ATA バージョン 1.6 移行ガイド](ata-update-1.6-migration-guide.md)

[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


