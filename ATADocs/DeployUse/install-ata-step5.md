---
# required metadata

title: ATA のインストール - 手順 5 | Microsoft Advanced Threat Analytics
description: ATA のインストールの手順 5 では、ATA ゲートウェイの設定を構成します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 5

>[!div class="step-by-step"] [« 手順 4](install-ata-step4.md)
[手順 6 »](install-ata-step6.md)


## 手順 5. ATA ゲートウェイの設定を構成する
ATA ゲートウェイがインストールされたら、次の手順を実行して、ATA ゲートウェイの設定を構成します。

1.  ATA コンソールで **[構成]** をクリックして、**[ATA ゲートウェイ]** ページを選択します。

2.  次の情報を入力します。

  - **説明**: <br>ATA ゲートウェイの説明を入力します (省略可能)。
  - **ポート ミラーリングされたドメイン コントローラー (FQDN)** (ATA ゲートウェイでは必須ですが ATA Lightweight Gateway に対しては設定できません): <br>ドメイン コントローラーの完全な FQDN を入力し、プラス記号をクリックして一覧に追加します。 例: **dc01.contoso.com**<br /><br />![FDQN のサンプル画像](media/ATAGWDomainController.png)

次の情報が、**[ドメイン コントローラー]** ボックスの一覧で入力したサーバーに適用されます。 -   トラフィックが ATA ゲートウェイによりポート ミラーリングを介して監視されているドメイン コントローラーはすべて、**[ドメイン コントローラー]** ボックスの一覧に表示されます。 **[ドメイン コントローラー]** ボックスの一覧にドメイン コントローラーが表示されていない場合は、疑わしいアクティビティの検出が想定どおり機能しない可能性があります。
-   リスト内の少なくとも 1 つのドメイン コントローラーを、グローバル カタログ サーバーにしてください。 これにより、ATA はフォレストの他のドメイン内のコンピューターとユーザー オブジェクトを解決します。

 - **キャプチャ ネットワーク アダプター** (必須):<br>
     - 専用サーバー上にある ATA ゲートウェイについては、構成済みのネットワーク アダプターを接続先ミラー ポートとして選択します。 これらのアダプターは、ミラー化されたドメイン コントローラーのトラフィックを受信します。
     - ATA Lightweight Gateway の場合、これは、組織内の他のコンピューターとの通信に使用するすべてのネットワーク アダプターにする必要があります。

![ゲートウェイ設定の画像](media/ATA-Config-GW-Settings.jpg)

 - **ドメイン シンクロナイザー候補**<br>
ドメイン シンクロナイザー候補に設定された ATA ゲートウェイはすべて、ATA と Active Directory ドメイン間の同期を担当できるようになります。 最初の同期は、ドメインのサイズによっては時間がかかり、また多くのリソースが必要になります。デフォルトでは、ATA ゲートウェイのみがドメイン シンクロナイザー候補に設定されます。 <br>リモート サイトの ATA ゲートウェイについては、ドメイン シンクロナイザー候補の設定を無効化することをお勧めします。<br>読み取り専用のドメイン コントローラーは、ドメイン シンクロナイザー候補に設定しないでください。 詳細については、「[ATA アーキテクチャ](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features)」を参照してください。

> [!NOTE] ATA ゲートウェイ サービスの初回起動では、ネットワーク キャプチャ パーサーのキャッシュが構築されるため、起動には数分かかります。<br>
構成の変更は、ATA ゲートウェイと ATA センター間のスケジュールされた次回の同期時に、ATA ゲートウェイに反映されます。



    

3. (省略可能) [Syslog リスナーおよび Windows イベント転送コレクション](configure-event-collection.md)を設定します。 
4. 今後リリースされるバージョンで ATA センターの更新時にこの ATA ゲートウェイも自動で更新されるように、**[ATA ゲートウェイを自動更新する]** を有効にします。
3.  **[保存]** をクリックします。


## インストールの検証
ATA ゲートウェイが正常に展開されたことを検証するには、以下を確認します。

1.  **Microsoft Advanced Threat Analytics Gateway** という名前のサービスが実行されていることを確認します。 ATA ゲートウェイの設定を保存した後、サービスの起動に数分かかる場合があります。

2.  サービスが起動されていない場合は、デフォルトのフォルダー (%programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs) に配置されている Microsoft.Tri.Gateway-Errors.log ファイルを確認します。

3.  詳細については、[ATA のトラブルシューティング](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors)に関するページを参照してください。

4.  これが最初にインストールした ATA ゲートウェイである場合、数分経ってから ATA コンソールにログインし、開いた画面の右側をスワイプして通知ウィンドウを開きます。 コンソールの右側にある通知バーに、**最近学習したエンティティ**の一覧が表示されます。

5.  デスクトップで **Microsoft Advanced Threat Analytics** のショートカットをクリックして、ATA コンソールに接続します。 ATA センターのインストールに使用したのと同じユーザー資格情報でログインします。
6.  コンソールの検索バーで、ドメイン上のユーザー、グループなどを検索します。
7.  パフォーマンス モニターを開きます。 パフォーマンス ツリーで **[パフォーマンス モニター]** をクリックし、プラス アイコンをクリックして、**カウンターを追加**します。 **Microsoft ATA ゲートウェイ**を展開し、**[Network Listener PEF Captured Messages/Sec (ネットワーク リスナー PEF がキャプチャしたメッセージ数/秒)]** までスクロールして追加します。 グラフにアクティビティが表示されます。

    ![パフォーマンス カウンターの追加のイメージ](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"] [« 手順 4](install-ata-step4.md)
[手順 6 »](install-ata-step6.md)

## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO3-->


