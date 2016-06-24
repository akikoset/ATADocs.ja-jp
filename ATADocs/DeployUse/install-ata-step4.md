---
# required metadata

title: ATA のインストール - 手順 4 | Microsoft Advanced Threat Analytics
description: ATA のインストールの手順 4 では、ATA ゲートウェイをインストールします。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 4

>[!div class="step-by-step"]
[« 手順 3](install-ata-step3.md)
[手順 5 »](install-ata-step5.md)

## 手順 4. ATA ゲートウェイをインストールする

ATA ゲートウェイを専用サーバーにインストールする前に、ポート ミラーリングが正しく構成されていること、ATA ゲートウェイがドメイン コントローラーとの間のトラフィックを認識できることを検証します。 詳細については、「[ポート ミラーリングの検証](validate-port-mirroring.md)」を参照してください。


> [!IMPORTANT]
> [KB2919355](http://support.microsoft.com/kb/2919355/) がインストールされていることを確認します。  次の PowerShell コマンドレットを実行して、修正プログラムがインストールされているかどうかを確認します。
>
> `Get-HotFix -Id kb2919355`

ATA ゲートウェイ サーバーで次の手順を実行します。

1.  zip ファイルからファイルを展開します。 
> [!NOTE] zip ファイルから直接インストールすると失敗します。

2.  管理者特権でのコマンド プロンプトから**Microsoft ATA Gateway Setup.exe** を実行し、セットアップ ウィザードに従います。

3.  **[ようこそ]**ページで使用する言語を選択し、**[次へ]** をクリックします。.

4.  **[ATA ゲートウェイ構成]** で、使用している環境に基づいて次の情報を入力します。

    ![ATA ゲートウェイ構成の画像](media/ATA-Gateway-Configuration.JPG)

    |フィールド|説明|コメント|
    |---------|---------------|------------|
    |インストール パス|ATA ゲートウェイをインストールする場所です。 既定では %programfiles%\Microsoft Advanced Threat Analytics\Gateway です。|既定値のままにします。|
    |ATA ゲートウェイ サービスの SSL 証明書|ATA ゲートウェイ サービスによって使用される証明書です。|ラボ環境のみの場合は、自己署名証明書を使用します。|
    |ATA ゲートウェイの登録|ATA 管理者のユーザー名とパスワードを入力します。|ATA センターに登録する ATA ゲートウェイについては、ATA センターをインストールしたユーザーのユーザー名とパスワードを入力します。 このユーザーは、ATA センターで次のローカル グループのいずれかのメンバーである必要があります。<br /><br />-   管理者<br />-   Microsoft Advanced Threat Analytics 管理者 **注:** これらの資格情報は登録のためにのみ使用され、ATA には保存されません。|
    ATA ゲートウェイのインストールでは、次のコンポーネントがインストールおよび構成されます。

    -   KB 3047154

        > [!IMPORTANT]
        > -   仮想化ホスト上に KB 3047154 をインストールしないでください (仮想化を実行しているホストの場合は、仮想マシン上で実行しても問題ありません)。 ポート ミラーリングが正常に動作しなくなる可能性があります。 
        > -   ATA ゲートウェイに Message Analyzer、Wireshark、またはその他のネットワーク キャプチャ ソフトウェアをインストールしないでください。 ネットワーク トラフィックをキャプチャする必要がある場合は、Microsoft Network Monitor 3.4 をインストールして使用してください。

    -   ATA ゲートウェイ サービス

    -   Microsoft Visual C++ 2013 再頒布可能パッケージ

    -   カスタム パフォーマンス モニターのデータ コレクション セット

5.  インストールが完了したら、ATA ゲートウェイの場合は**[起動]** をクリックしてブラウザーを開き、ATA コンソールにログインします。 ATA 簡易ゲートウェイの場合は**[完了]**をクリックします。.


>[!div class="step-by-step"]
[« 手順 3](install-ata-step3.md)
[手順 5 »](install-ata-step5.md)

## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


