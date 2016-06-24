---
# required metadata

title: ATA バージョン 1.4 の新機能 | Microsoft Advanced Threat Analytics
description: ATA バージョン 1.4 の新機能と既知の問題を示します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA バージョン 1.4 の新機能
このリリース ノートは、Advanced Threat Analytics のバージョン 1.4 の既知の問題に関する情報を提供します。

## このバージョンの新機能

-   イベントをドメイン コントローラーから ATA ゲートウェイに直接送信する Windows Event Forwarding (WEF) のサポート。

-   DPI (詳細なパケット検査) と Windows イベント ログの組み合わせによる企業リソースに対する Pass-the-Hash 検出の強化。

-   ドメインに参加していないデバイスと Windows 以外のデバイスでの検出と可視性のサポートの強化。

-   ATA ゲートウェイごとにより多くのトラフィックをサポートするためのパフォーマンスの向上。

-   ATA センターごとにより多くの ATA ゲートウェイをサポートするためのパフォーマンスの向上。

-   コンピューター名と IP アドレスを一致させる新しい自動名前解決プロセスの追加。この独自の機能は、調査プロセス中の貴重な時間を節約し、セキュリティ分析のための強力な証拠を提供します。

-   ユーザーからの入力を収集して、検出プロセスを自動的に調整する機能の向上。

-   NAT デバイスの自動検出。

-   ドメイン コントローラーに到達できない場合の自動フェールオーバー。

-   システム正常性の監視と通知でのデプロイの全体的な正常性の状態と構成と接続に関連する特定の問題の提示。

-   エンティティが動作しているサイトと場所の表示。

-   マルチドメインのサポート。

-   単一ラベル ドメイン (SLD) のサポート。

-   ATA ゲートウェイと ATA センターの IP アドレスと証明書の変更のサポート。

-   カスタマー エクスペリエンスの向上に役立つ製品利用統計情報。

## 既知の問題
このバージョンには、以下の既知の問題があります。

### ネットワーク キャプチャ ソフトウェア
ATA ゲートウェイにインストールできる唯一のサポートされているネットワーク キャプチャ ソフトウェアは [Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865) です。 Microsoft Message Analyzer またはその他のネットワーク キャプチャ ソフトウェアをインストールしないでください。 その他のソフトウェアをインストールすると、ATA ゲートウェイが正しく機能しなくなります。

### Zip ファイルからのインストール
ATA ゲートウェイをインストールするときは、zip ファイルからローカル ディレクトリにファイルを抽出し、そこからインストールしてください。 zip ファイルから直接 ATA ゲートウェイをインストールしないでください。直接実行すると、インストールは失敗します。

### ATA の以前のバージョンのアンインストール
ATA の以前のバージョン、パブリック プレビュー版、またはプライベート プレビュー版をインストールしている場合は、ATA の今回のリリースをインストールする前に、ATA センターと ATA ゲートウェイをアンインストールする必要があります。

データベース ファイルとログ ファイルも削除する必要があります ATA の以前のバージョンのデータベースは、ATA の GA バージョンと互換性がありません。

ATA センターまたは ATA ゲートウェイをアンインストールしようとしたときに、アンインストールでは ATA のインストールが開く場合は、次のレジストリ キーを追加した後、もう一度 ATA をアンインストールする必要があります。

**ATA センター**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   `InstallationPath` という名前で、値が `C:\Program Files\Microsoft Advanced Threat Analytics\Center` である新しい文字列値を追加します。 これは既定のインストール フォルダーです。 インストール フォルダーを変更した場合は、ATA がインストールされているパスを入力します。

    ![ATA センターのインストール パス用のレジストリ エディター](media/ATA-uninstall-center-bug.jpg)

**ATA ゲートウェイ**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   `InstallationPath` という名前で、値が `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway` である新しい文字列値を追加します。 これは既定のインストール フォルダーです。  インストール フォルダーを変更した場合は、ATA がインストールされているパスを入力します。

    ![ATA ゲートウェイのインストール パス用のレジストリ エディター](media/ATA-GW-uninstall-bug.jpg)

アンインストールした後、ATA センターと ATA ゲートウェイのインストール フォルダーを両方とも削除します。  データベースを別のフォルダーにインストールしている場合は、ATA センターのデータベース フォルダーを削除します。

### 正常性アラート - ATA ゲートウェイを切断しました
1 つ以上の ATA ゲートウェイがある場合に、ATA ゲートウェイ切断アラートが発生した場合、自動解決はそれらの 1 つのみで機能し、残りはオープン状態のままになります。 ATA ゲートウェイが稼働し、サービスが実行されていることを手動で確認し、アラートを手動で解決する必要があります。

### 仮想化ホスト上の KB
仮想化ホスト上に KB 3047154 をインストールしないでください。 ポート ミラーリングが正常に動作しなくなる可能性があります。

## 関連項目

[ATA バージョン 1.6 移行ガイド](ata-update-1.6-migration-guide.md)

[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


