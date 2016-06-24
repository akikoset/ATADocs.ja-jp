---
# required metadata

title: ATA コンソールの操作 | Microsoft Advanced Threat Analytics
description: ATA コンソールにログインする方法と、コンソールのコンポーネントについて説明します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1bf264d9-9697-44b5-9533-e1c498da4f07

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA コンソールの使用

ATA コンソールを使用して監視を行い、ATA によって検出された不審なアクティビティに応答します。

## ATA コンソールにアクセスできるようにする
ATA センター サーバーでローカルのAdministrators グループのメンバーであるユーザーは、ATA コンソールにログインし、ATA 設定を管理する権限があります。
ローカル管理者でないユーザーが ATA コンソールにログインできるようにするには、ローカル グループ **Microsoft Advanced Threat Analytics Administrators** にユーザーを追加します。

## ATA コンソールへのログイン

1. ATA センター サーバーで、デスクトップの **Microsoft ATA コンソール**のアイコンをクリックするか、ブラウザーを開いて ATA コンソールにアクセスします。

    ![ATA サーバー アイコン](media/ata-server-icon.png)

    > [!NOTE]ATA センターまたは ATA ゲートウェイからブラウザーを開き、ATA センターのインストールで ATA コンソール用に構成した IP アドレスにアクセスすることもできます。    

2.  ユーザー名とパスワードを入力し、**[ログイン]** をクリックします。

![ATA ログイン画面のイメージ](media/ATA-log-in-screen.jpg)

    > [!NOTE]
    > You have to log in with a user who is a member of the local administrator group OR of the Microsoft Advanced Threat Analytics Administrators group.

## ATA コンソール

ATA コンソールでは、すべての不審なアクティビティを時系列順にすばやく確認することができます。 各アクティビティの詳細を確認して、アクティビティに応じた対応を講じることができます。 コンソールには、ATA ネットワークの問題や疑わしいと思われる新しいアクティビティを表面化するアラートと通知も表示されます。

ATA コンソールの主要な要素を次に示します。


### 攻撃タイムライン

これは、ATA コンソールにログインしたときに表示される既定のランディング ページです。 既定では、すべてのオープン状態である不審なアクティビティが攻撃タイムラインに表示されます。 攻撃タイムラインをフィルター処理して、オープン、破棄済み、または解決済み状態のアクティビティを表示できます。 各アクティビティに割り当てられた重大度を確認することもできます。

![ATA 攻撃タイムラインの画像](media/attack-timeline.png)

詳細については、「[不審なアクティビティの処理](/advanced-threat-analytics/deploy-use/working-with-suspicious-activities)」を参照してください。

### 通知バー

新しい不審なアクティビティが検出されると、通知バーが右側に自動的に開きます。 前回のログオン以降に新しい不審なアクティビティがある場合は、ログインに成功した後で通知バーが開きます。 通知バーには、右側にある矢印をクリックするといつでもアクセスできます。

![ATA 通知バーの画像](media/notification-bar.png)

### フィルター処理パネル

攻撃タイムラインまたはエンティティ プロファイルの不審なアクティビティ タブに表示する不審なアクティビティを、状態または重大度に基づいてフィルター処理できます。

### 検索バーを非表示にする

上部のメニューには、検索バーがあります。 ATA の特定のユーザー、コンピューター、またはグループを検索できます。 入力を開始して試しください。

![ATA コンソールの検索の画像](media/ATA-console-search.png)

### ヘルス センター

ヘルス センターでは、ATA 展開内で異常が生じている場合にアラートが表示されます。

![ATA ヘルス センターの画像](media/health-center.png)

接続エラーや ATA ゲートウェイの切断などの問題がシステムで発生すると、ヘルス センター アイコンに赤い点が表示されます。 ![ATA ヘルス センターの赤色のドットのイメージ](media/ATA-Health-Center-Alert-red-dot.png)

ヘルス センターのアラートは破棄するか解決でき、重大度に応じて高、中、低に分類されます。 ATA サービスがまだアクティブであると検出しているアラートを解決した場合、アラートは自動的にオープン リストに移動されます。 システムがアラートの原因がなくなった (状況が修正された) ことを検出した場合、アラートは自動的に解決済みリストに移動されます。

### ユーザー プロファイルとコンピューター プロファイル

ATA では、ネットワーク内の各ユーザーとコンピューターのプロファイルが作成されます。 ATA のユーザー プロファイルでは、グループのメンバーシップ、最近のログイン、最近アクセスしたリソースなどの一般的な情報が表示されます。

![ユーザー プロファイル](media/user-profile.png)

ATA のコンピューター プロファイルでは、グループのメンバーシップ、最近のログインや最近アクセスされたリソースなどの一般的な情報が表示されます。

![コンピューター プロファイル](media/computer-profile.png)

各エンティティ (コンピューター、デバイス、ユーザー) に関する詳細情報は、[概要]、[アクティビティ]、[疑わしいアクティビティ] ページに表示されます。

ATA が完全に解決できていないプロファイルは、円を半分塗りつぶしたアイコンで識別されます。


![ATA のオープン プロファイルの画像](media/ATA-Unresolved-Profile.jpg)

### ミニ プロファイル

ユーザーやコンピューターなどのエンティティが 1 つだけ表示されているコンソールの場所では、そのエンティティ上にマウスを移動すると、ミニ プロファイルが自動的に開いて次の情報が表示されます (入手できる場合)。

![ATA のミニ プロファイルの画像](media/ATA-mini-profile.jpg)

-   名前

-   画像

-   電子メール

-   電話

-   重大度別の不審なアクティビティの数



## 関連項目
[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


