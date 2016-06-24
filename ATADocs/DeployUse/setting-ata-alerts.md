---
# required metadata

title: ATA 通知の設定 | Microsoft Advanced Threat Analytics
description: 疑わしいアクティビティが検出されたときに通知されるように ATA アラートを設定する方法について説明します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 通知の設定
ATA では、疑わしいアクティビティを検出した場合、電子メールにより、または ATA イベント転送を使用するか、イベントを SIEM/Syslog サーバーに転送して通知を受信できます。 受信を希望する通知を選択する前に、[電子メール サーバーと Syslog サーバーの設定](setting-syslog-email-server-settings.md)を行います。

> [!NOTE]
> -   電子メール通知に記載されたリンクにより、検出された疑わしいアクティビティに直接アクセスできます。 リンクのホスト名部分は、ATA センター ページの ATA コンソール URL の設定から取得されます。 既定では、ATA コンソール URL は、ATA センターのインストール時に選択した IP アドレスです。  電子メール通知を構成する場合は、ATA コンソール URL として FQDN を使用することをお勧めします。
> -   通知は、ATA センターから SMTP サーバーまたは Syslog サーバーのいずれかに送信されます。

電子メール通知を受信するには、次のように設定します：


1. ATA コンソールでツール バーの設定オプションを選択し、**[構成]** を選択します。
![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

2. **[通知]**を選択します。
3. **[電子メール通知]**で切り替えを使用し、送信される通知を選択します:


    - 新たな疑わしいアクティビティが検出されました
    - 正常性に関する新たな問題が検出されました
    - 新しいソフトウェア更新プログラムが利用可能です

4. 電子メールで通知を受け取る受信者を指定します。

    注：疑わしいアクティビティ向けの電子メール アラートが送信されるのは、疑わしいアクティビティが作成されたときのみです。


5. **[保存]** をクリックします。

Syslog の通知を受信するには、次のように設定します：


1. ATA コンソールでツール バーの設定オプションを選択し、**[構成]** を選択します。
![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

2. **[通知]**を選択します。
3. **[Syslog の通知]**で切り替えを使用し、送信される通知を選択します:


    - 新たな疑わしいアクティビティが検出されました
    - 既存の疑わしいアクティビティを更新します
    - 正常性に関する新たな問題が検出されました
5. **[保存]** をクリックします。
![ATA 通知設定の画像](media/ATA-notification-settings.png)




## 関連項目
[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Jun16_HO1-->


