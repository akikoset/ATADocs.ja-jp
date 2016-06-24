---
# required metadata

title: ATA のインストール - 手順 1 | Microsoft Advanced Threat Analytics
description: ATA のインストールの手順 1 では、選択したサーバーに ATA センターをダウンロードしてインストールします。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 1

>[!div class="step-by-step"]

[手順 2 »](install-ata-step2.md)

このインストール手順では、ATA 1.6 の新規インストールを実行するための手順を示します。 ATA の既存の展開を旧バージョンから更新する方法については、「 [ATA migration guide for version 1.6 (ATA バージョン 1.6 の移行ガイド)](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide)」をご覧ください。

> [!IMPORTANT] インストールを開始する前に ATA センター サーバーと ATA ゲートウェイ サーバーに KB2934520 をインストールします。そうしないと、ATA のインストール時にこの更新プログラムがインストールされ、ATA のインストールの途中で再起動が必要になります。

## 手順 1. ATA センターをダウンロードしてインストールする
サーバーが要件を満たしていることを確認したら、ATA センターのインストールを続行できます。

ATA センター サーバーで次の手順を実行します。

1.  [Microsoft ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)、[TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/)、または [MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads) から ATA をダウンロードします。

2.  ATA センターをインストールするコンピューターに、ローカル管理者グループのメンバーであるユーザーとしてログインします。

3.  **Microsoft ATA Center Setup.EXE** を実行し、セットアップ ウィザードの手順に従います。

4.  Microsoft .Net Framework がインストールされていない場合、ATA センターのインストールの開始時にインストールするように求められます。 .NET Framework をインストールすると、再起動するように求められる場合があります。
5.  **[ようこそ]** ページで、ATA のインストール画面で使用する言語を選択し、**[次へ]** をクリックします。

6.  マイクロソフト ソフトウェア ライセンス条項を読み、この条項に同意する場合は、チェックボックスをクリックして、**[次へ]** をクリックします。

7.  更新を自動で行うように ATA を設定することをお勧めします。 コンピューターの Windows が自動更新を行うように設定されていない場合は、**[Microsoft Update を使用すると、コンピューターをセキュリティで保護された最新の状態に保つことができます]** 画面が表示されます。 
    ![ATA の更新画像](media/ata_ms_update.png)

8. **[Microsoft Update を使用して更新プログラムを確認する (推奨)]** を選択します。 これで、次に示すように、他の Microsoft 製品 (ATA を含む) の更新を有効化できるように Windows の設定が変更されます。 
    ![Windows 自動更新の画像](media/ata_installupdatesautomatically.png)

8.  **[ATA センターの構成]** ページで、使用している環境に基づいて次の情報を入力します。

    |フィールド|説明|コメント|
    |---------|---------------|------------|
    |インストール パス|ATA センターをインストールする場所です。 既定では %programfiles%\Microsoft Advanced Threat Analytics\Center です。|既定値のままにします。|
    |データベースのデータ パス|MongoDB データベース ファイルが配置される場所です。 既定では %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data です。|サイズ変更に基づいて、拡張する余裕のある場所に変更します。 **注:** <ul><li>運用環境では、容量計画に基づいて、十分な空き領域があるドライブを使用する必要があります。</li><li>大規模な展開では、データベースは別の物理ディスク上にある必要があります。</li></ul>サイズの詳細については、「[ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)」をご覧ください。|
    |ATA センター サービスの IP アドレス: ポート|ATA センター サービスが ATA ゲートウェイからの通信をリッスンする IP アドレスです。<br /><br />**既定のポート:** 443|下方向キーをクリックして、ATA センター サービスによって使用される IP アドレスを選択します。<br /><br />ATA センター サービスの IP アドレスとポートを、ATA コンソールの IP アドレスとポートと同じにすることはできません。 ATA コンソールのポートを変更するようにしてください。|
    |ATA センター サービスの SSL 証明書|ATA センター サービスによって使用される証明書です。|鍵のアイコンをクリックしてインストールされている証明書を選択するか、ラボ環境で展開する場合は自己署名証明書のチェックボックスをオンにします。|
    |ATA コンソールの IP アドレス|ATA コンソール用の IIS によって使用される IP アドレスです。|下方向キーをクリックして、ATA コンソールによって使用される IP アドレスを選択します。 **注:** ATA ゲートウェイから ATA コンソールにアクセスしやすくには、この IP アドレスを書き留めておいてください。|
    |ATA コンソールの SSL 証明書|IIS によって使用される証明書です。|鍵のアイコンをクリックしてインストールされている証明書を選択するか、ラボ環境で展開する場合は自己署名証明書のチェックボックスをオンにします。|

    ![ATA センター構成の画像](media/ATA-Center-Configuration.JPG)

10.  **[インストール]** をクリックして、ATA センターとそのコンポーネントをインストールします。
    ATA センターのインストールでは、次のコンポーネントがインストールおよび構成されます。

    -   インターネット インフォメーション サービス (IIS)

    -   ATA センター サービスと ATA コンソールの IIS サイト

    -   MongoDB

    -   カスタム パフォーマンス モニターのデータ コレクション セット

    -   自己署名証明書 (インストール時に選択した場合)

11.  インストールが完了したら、**[起動]** をクリックして ATA コンソールに接続します。
この時点では、自動的に **[一般設定]** ページに移動し、ATA ゲートウェイの構成と展開を続行することになります。
IP アドレスを使用してサイトにログインしているため、証明書に関する警告が表示されます。これは正常な動作ですので、**[このサイトの閲覧を続行する]** をクリックしてください。

### インストールの検証

1.  **Microsoft Advanced Threat Analytics Center** という名前のサービスが実行されていることを確認します。
2.  デスクトップで **Microsoft Advanced Threat Analytics** のショートカットをクリックして、ATA コンソールに接続します。 ATA センターのインストールに使用したのと同じユーザー資格情報でログインします。



>[!div class="step-by-step"] [«インストールの前](preinstall-ata.md)
[手順 2 »](install-ata-step2.md)

## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO4-->


