---
# required metadata

title: ATA のインストール | Microsoft Advanced Threat Analytics
description: ATA のインストールの最後の手順では、短期リース サブネットとハニートークン ユーザーを構成します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA のインストール - 手順 6

>[!div class="step-by-step"]
[« 手順 5](install-ata-step5.md)

## 手順 6. 短期リース サブネットとハニートークン ユーザーを構成する
短期リース サブネットは、IP アドレスの割り当てが急速に (秒または分刻みで) 変わるサブネットです。 VPN や Wi-Fi IP アドレスに使用される IP アドレスなどがあります。 組織で使用する短期リース サブネットの一覧を入力するには、次の手順を実行します。

1.  ATA ゲートウェイ コンピューター上の ATA コンソールで、設定アイコンをクリックして**[構成]** を選択します。.

    ![ATA 構成の設定](media/ATA-config-icon.JPG)

2.  **[検出]** で、短期リース サブネットについて以下を入力します。 スラッシュ表記を使用して短期リース サブネットを入力し (例: `192.168.0.0/24`)、プラス記号をクリックします。

3.  ハニートークン アカウント SID の場合は、ネットワーク アクティビティを持たないユーザー アカウントの SID を入力し、プラス記号をクリックします。 たとえば、 `S-1-5-21-72081277-1610778489-2625714895-10511`.

    > [!NOTE]
    > ユーザーの SID を検索するには、ATA コンソールでユーザーを検索して **[アカウント情報]** タブをクリックします。 

4.  除外リストの構成: IP アドレスを特定の疑わしいアクティビティから除外するように構成できます。 詳しくは、「[Working with ATA detection settings (ATA 検出設定の操作)](working-with-detection-settings.md)」を参照してください。

5.  **[保存]** をクリックします。.

![変更の保存](media/ATA-VPN-Subnets.JPG)

これで、Microsoft Advanced Threat Analytics が無事に展開されました。

検出された疑わしいアクティビティを表示するには攻撃タイムラインを確認し、ユーザーまたはコンピューターを検索して、プロファイルを表示します。

ATA が疑わしいアクティビティのスキャンを直ちに開始します。 疑わしい動作のアクティビティなど一部のアクティビティ は、ATA が動作プロファイルを作成するまでは (最低 3 週間) 利用できません。


>[!div class="step-by-step"]
[« 手順 5](install-ata-step5.md)


## 関連項目

- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [イベント コレクションの構成](configure-event-collection.md)
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=May16_HO1-->


