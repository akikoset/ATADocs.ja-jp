---
# required metadata

title: ATA 構成の変更 - ATA コンソールの IP アドレス | Microsoft Advanced Threat Analytics
description: ATA ゲートウェイ上の ATA コンソールへのショートカットを作成するために使用する、ATA コンソールの IP アドレスを変更する方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 構成の変更 - ATA コンソールの IP アドレス

>[!div class="step-by-step"]
[« ATA センター証明書](modifying-ata-config-centercert.md)
[IIS 証明書 »](modifying-ata-config-iiscert.md)

## ATA コンソールの IP アドレスを変更する
既定では、ATA コンソールの URL は、ATA センターのインストール時に ATA コンソール IP アドレスに選択した IP アドレスです。

URL は次のようなシナリオで使用されます。

-   ATA ゲートウェイのインストール – ATA ゲートウェイがインストールされるとき、ゲートウェイは自らを ATA センターに登録します。 この登録プロセスは、ATA コンソールに接続することにより実行されます。 ATA コンソール URL の FQDN を入力する場合、ATA ゲートウェイで、ATA コンソールが IIS にバインドされている IP アドレスに FQDN を解決できることを確認する必要があります。 さらに、URL を使用して、ATA ゲートウェイに ATA コンソールへのショートカットを作成します。

-   アラート – ATA は SIEM または電子メール アラートを送信するとき、疑わしいアクティビティへのリンクを含めます。 リンクのホスト部分は、ATA コンソール URL の設定です。

-   社内の証明機関 (CA) から証明書をインストールした場合、ATA コンソールへの接続時にユーザーが警告メッセージを受け取らないように、URL と証明書のサブジェクト名との照合が必要になる場合があります。

-   ATA コンソール URL の FQDN を使用することで、IIS が ATA コンソール用に使用する IP アドレスを、過去に送信されたアラートを解除したり、ATA ゲートウェイ パッケージを再度ダウンロードすることなく変更することができます。 必要があるのは、DNS を新しい IP アドレスで更新することだけです。

> [!NOTE]
> ATA コンソール URL を変更したら、新しい ATA ゲートウェイをインストールする前に、ATA ゲートウェイ セットアップ パッケージをダウンロードする必要があります。

ATA コンソール用に IIS によって使用される IP アドレスを変更する必要がある場合は、ATA センター サーバーで次の操作を実行します。

1.  ATA センター サーバーに IP アドレスをインストールします。

2.  インターネット インフォメーション サービス (IIS) マネージャーを開きます。

3.  サーバーの名前を展開し、**[サイト]** を展開します。.

4.  Microsoft ATA コンソールのサイトを選択し、[**Actions (アクション)**] ウィンドウで **[バインド]** をクリックします。.

    ![ATA コンソールのバインド操作のイメージ](media/ATA-console-change-IP-bindings.jpg)

5.  **[HTTP]** を選択し、**[編集]** をクリックして、新しい IP アドレスを選択します。 **HTTPS** についても同じ操作を行い、同じ IP アドレスを選択します。

    ![サイト バインドの編集イメージ](media/ATA-change-console-IP.jpg)

6.  **[Action (アクション)]** ペインで、**[Web サイトの管理]** の **[再起動]** をクリックします。.

7.  管理者コマンド プロンプトを開き、次のコマンドを入力して、HTTP.SYS ドライバーを更新します。

    -   新しい IP アドレスを追加するには -  `netsh http add iplisten ipaddress=newipaddress`

    -   新しいアドレスが使用されていることを確認するには -  `netsh http show iplisten`

    -   古い IP アドレスを削除するには –  `netsh http delete iplisten ipaddress=oldipaddress`

8.  ATA コンソール URL で IP アドレスがまだ使用される場合は、新しい ATA を展開する前に、ATA コンソール URL を新しい IP アドレスに更新し、ATA ゲートウェイ セットアップ パッケージをダウンロードします。

9. ATA コンソール URL が FQDN である場合は、DNS を FQDN の新しい IP アドレスに更新します。

>[!div class="step-by-step"]
[« ATA センター証明書](modifying-ata-config-centercert.md)
[IIS 証明書 »](modifying-ata-config-iiscert.md)


## 参照
- [ATA コンソールの使用](working-with-ata-console.md)
- [ATA のインストール](install-ata.md)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


