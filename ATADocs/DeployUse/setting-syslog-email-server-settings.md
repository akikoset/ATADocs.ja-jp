---
# required metadata

title: ATA 通知の設定 | Microsoft Advanced Threat Analytics
description: 疑わしいアクティビティが検出されたとき、ATA 通知をどのように受け取るか (電子メールまたは ATA イベント転送を使用) について説明します。 
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

## ATA に電子メール サーバーの設定を入力する
ATA は、疑わしいアクティビティを検出したときに通知を生成できます。 ATA が電子メール通知を送信できるようにするには、まず **[電子メール サーバーの設定]**を構成します。.

1.  ATA センター サーバーで、デスクトップ上の **Microsoft Advanced Threat Analytics 管理**アイコンをクリックします。

2.  ユーザー名とパスワードを入力し、**[ログイン]** をクリックします。.

3.  ツール バーの設定オプションを選択し、**[構成]** を選択します。.

    ![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

4.   **[全般]**タブの**[電子メール サーバー]**に、次の情報を入力します：

    |フィールド|説明|値|
    |---------|---------------|---------|
    |SMTP サーバー エンドポイント (必須)|SMTP サーバーの FQDN を入力します。|例:<br />smtp.contoso.com|
    |SSL|SMTP サーバーに SSL が必要な場合は、SSL に切り替えます。 **注:** SSL を有効にした場合、ポート番号も変更する必要があります。|既定では無効になっています|
    |認証|SMTP サーバーに認証が必要な場合に有効にします。 **注:** 認証を有効にした場合に、SMTP サーバーに接続する権限を持つ電子メール アカウントのユーザー名とパスワードを入力する必要があります。|既定では無効になっています|
    |Send from (送信元) (必須)|電子メールの送信元の電子メール アドレスを入力します。|例:<br />ATA@contoso.com|
    ![ATA 電子メール サーバー設定の画像](media/ATA-email-server.png)

## ATA に Syslog サーバーの設定を入力する
ATA では、疑わしいアクティビティを検出した場合に Syslog サーバーに通知を送信することにより通知を生成できます。 Syslog 通知を有効にした場合、通知の以下の設定を指定できます。

1.  Syslog 通知を構成する前に、SIEM 管理者と協力して次の情報を取得します：

    -   SIEM サーバーの FQDN または IP アドレス

    -   SIEM サーバーがリッスンするポート

    -   使用するトランスポート：UDP、TCP または TLS (セキュリティ保護された Syslog)

    -   データ RFC 3164 または 5424 の送信に使用する形式

2.  ATA センター サーバーで、デスクトップ上の **Microsoft Advanced Threat Analytics 管理**アイコンをクリックします。

3.  ユーザー名とパスワードを入力し、**[ログイン]** をクリックします。.

4.  ツール バーの設定オプションを選択し、**[構成]** を選択します。.

    ![ATA 構成設定アイコン](media/ATA-config-icon.JPG)

5.  **[Syslog サーバー]** を選択して次の情報を入力します:

    |フィールド|説明|
    |---------|---------------|
    |Syslog サーバー エンドポイント|Syslog サーバーの FQDN|
    |トランスポート|UDC、TCP または TLS (セキュリティ保護された Syslog)|
    |Format (形式)|イベントを SIEM サーバーに送信するために ATA によって使用される形式 - RFC 5424 または RFC 3164 のいずれか。|





## 関連項目
[ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


