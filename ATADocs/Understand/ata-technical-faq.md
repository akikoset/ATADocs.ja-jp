---
# required metadata

title: ATA に関してよく寄せられる質問 | Microsoft Advanced Threat Analytics
description: ATA に関してよく寄せられる質問とその回答を示します。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA に関してよく寄せられる質問
この記事では、ATA に関してよく寄せられる質問とその回答を示します。


## ATA のライセンスはどのように付与されますか?
ライセンスの情報については、「[Advanced Threat Analytics の購入方法](https://www.microsoft.com/en-us/server-cloud/products/advanced-threat-analytics/Purchasing.aspx)」を参照してください。


## ATA ゲートウェイが起動しない場合はどうすればよいですか。
ATA のインストール先の "Logs" フォルダーにある現在のエラー ログで、一番新しいエラーを調べてください。
## ATA をテストするにはどうすればよいですか。
次のいずれかの方法で疑わしいアクティビティをシミュレートすることができます (エンド ツー エンドのテスト)。

1.  Nslookup.exe を使用した DNS 偵察
2.  psexec.exe を使用したリモート実行


ATA ゲートウェイからではなく、監視されているドメイン コントローラーに対してリモートで実行する必要があります。

## Windows イベント転送を確認するにはどうすればよいですか。
ディレクトリ **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** からコマンド プロンプトを起動し、次のコマンドを実行します。

        mongo ATA --eval "printjson(db.getCollectionNames())" | find /C "NtlmEvents"`
## ATA で暗号化されたトラフィックを使用できますか。
暗号化されたトラフィックは分析されません (例: LDAPS、IPSEC ESP)。
## ATA で Kerberos 防御を使用できますか。
ATA は Kerberos 防御 (フレキシブル認証セキュア トンネリング (FAST) とも呼ばれます) をサポートしていますが、Overpass-the-Hash の検出はできません。
## ATA ゲートウェイはいくつ必要ですか。

まず、ATA Lightweight Gateway に対応するドメイン コントローラーで ATA Lightweight Gateway を使用することをお勧めします。ATA Lightweight Gateway に対応するドメイン コントローラーを特定するには、「[ATA Lightweight Gateway のサイズ変更](/advanced-threat-analytics/plan-design/ata-capacity-planning#ATA-Lightweight-Gateway-Sizing)」を参照してください。 

ATA Lightweight Gateway がすべてのドメイン コント ローラーに対応する場合、ATA ゲートウェイは必要ありません。

ATA Lightweight Gateway で対応できないドメイン コント ローラーについては、必要なATA ゲートウェイの数を決定する際に、次を考慮してください。

 - ドメイン コントローラーが生成するトラフィック量の合計、および (ポート ミラーリングを構成するための) ネットワーク アーキテクチャ。 ドメイン コントローラーが生成するトラフィック量を調べる方法の詳細については、「[ドメイン コントローラーのトラフィックの推定](/advanced-threat-analytics/plan-design/ata-capacity-planning#Domain-controller-traffic-estimation)」を参照してください。
 - ポート ミラーリングの運用上の制限もまた、ドメイン コントローラをサポートするために必要な ATA ゲートウェイの数に影響します。各環境にそれぞれ独自の考慮事項があります (例: スイッチごと、データ センターごと、リージョンごと)。 

## ATA に必要なストレージの容量を教えてください。
1 日あたり平均 1000 パケット/秒で 0.3 GB のストレージが必要です。<br /><br />ATA センターのサイズ変更の詳細については、「[ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)」を参照してください。


## 一部のアカウントが機密アカウントになっているのはなぜですか。
機密として指定されているグループ ("Domain Admins" など) のメンバーになっていると、そのアカウントもまた機密扱いになります。

アカウントのグループ メンバーシップを調べれば、どの機密グループに属しているかがわかります (直属のグループが別の機密グループに属しているために機密扱いになっている場合もあるので、最上位レベルの機密グループが見つかるまで、グループを上に上に遡って調べる必要があります)。

## ATA を使用して仮想ドメイン コントローラーを監視するにはどうすればよいですか。
仮想ドメイン コントローラーのほとんどは ATA Lightweight Gateway で対応できます。お使いの環境に ATA Lightweight Gateway が適しているかどうかを確認するには、「[ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)」を参照してください。

ATA Lightweight Gateway で対応できない仮想ドメイン コント ローラーがある場合は、「[ポート ミラーリングの構成](/advanced-threat-analytics/deploy-use/configure-port-mirroring)」の説明に従って、仮想または物理 ATA ゲートウェイを使用できます。  <br />最も簡単な方法は、仮想ドメイン コントローラーが存在するすべてのホストで仮想 ATA ゲートウェイを構成することです。<br />仮想ドメイン コントローラーがホスト間を移動する場合は、次のいずれかを実行する必要があります。

-   仮想ドメイン コントローラーが別のホストに移動する場合、最近移動した仮想ドメイン コントローラーからのトラフィックを受信できるよう、そのホストで ATA ゲートウェイを事前構成します。
-   仮想ドメイン コントローラーが移動したときに ATA ゲートウェイも一緒に移動するよう、仮想ドメイン コントローラーと仮想 ATA ゲートウェイを関連付けます。
-   ホスト間でトラフィックを送信できる仮想スイッチがいくつかあります。

## ATA をバックアップするにはどうすればよいですか。
次の 2 つをバックアップします。

-   ATA によって格納されるトラフィックとイベント。サポートされている任意のデータベース バックアップ手順を使用してバックアップすることができます。詳細については、「[ATA データベース管理](/advanced-threat-analytics/deploy-use/ata-database-management)」を参照してください。 
-   ATA の構成。データベースに格納され、1 時間ごとに自動的にバックアップされます。 

## ATA では何を検出できますか。
ATA は既知の悪意ある攻撃と手法、セキュリティ上の問題、およびリスクを検出します。
ATA で検出できるものの詳細な一覧については、「[Microsoft Advanced Threat Analytics とは何ですか?](what-is-ata.md)」を参照してください。

## ATA に必要なストレージの種類を教えてください。
待機時間の短いディスク アクセス (10 ミリ秒未満) による高速のストレージはをお勧めします (7,200 RPM ディスクは推奨されません)。 RAID 構成は、負荷の高い書き込みをサポートする必要があります (RAID 5/6 およびその派生物は推奨されません) 。

## ATA ゲートウェイに必要な NIC の数を教えてください。
ATA ゲートウェイには、少なくとも 2 つのネットワーク アダプターが必要です。<br>1.内部ネットワークと ATA センターに接続するための NIC<br>2.ポートのミラーリングを介したドメイン コントローラーのネットワーク トラフィックのキャプチャに使用される NIC<br>* これは、ドメイン コント ローラーが使用するすべてのネットワーク アダプターをネイティブに使用する ATA Lightweight Gateway には適用されません。

## ATA は SIEM とどのように統合できますか。
ATA では、次のように SIEM との双方向の統合が可能です。

1. 疑わしいアクティビティが発生したときに、CEF 形式を使用して任意の SIEM サーバーに Syslog アラートを送信するよう ATA を構成できます。
2. [これらの SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#SIEM-support) から、各 Windows イベントの Syslog メッセージ (ID 4776) を受信するよう ATA を構成できます。

## ATA は、IaaS ソリューション上で視覚化されたドメイン コント ローラーを監視できますか。

はい、ATA Lightweight Gateway を使用して、IaaS ソリューション内にあるドメイン コントローラを監視できます。

## オンプレミスとクラウドのどちらで提供されているのでしょうか?
Microsoft Advanced Threat Analytics は、オンプレミスの製品です。

## Azure Active Directory またはオンプレミスの Active Directory の一部として提供されるのでしょうか?
このソリューションはスタンドアロンで提供されます。Azure Active Directory やオンプレミスの Active Directory の一部としては提供されません。

## 独自の規則やしきい値、基準を作成する必要はありますか?
Microsoft Advanced Threat Analytics では、ルール、しきい値、基準の作成や後の微調整は不要です。 ATA はユーザー、デバイス、リソース間の行動や関係性を分析し、疑わしいアクティビティや既知の攻撃を迅速に検出します。 展開して 3 週間後、ATA は行動の疑わしいアクティビティの検出を開始します。 また一方で、ATA は既知の悪意のある攻撃やセキュリティ上の問題については展開直後から検出を開始します。

## 既に何らかの侵害を受けている場合でも、Microsoft Advanced Threat Analytics は異常行動を特定できますか?
はい、侵害を受けている状態で ATA をインストールした場合でも、ATA はハッカーによる疑わしいアクティビティを検出します。 ATA はユーザーの行動を見ているだけでなく、組織セキュリティ マップ内の他のユーザーに対しても目を配っています。 最初の分析時に攻撃者の行動が異常と見なされた場合、それは「外れ値」として認識され、ATA はその異常行動を常に報告します。 さらに、ATA はハッカーが別のユーザーの資格情報を盗もうとする (Pass-the-Ticket など) 場合や、ドメイン コントローラーの 1 つに対してリモート実行を試行する場合など、疑わしいアクティビティを検出できます。

## これは Active Directory からのトラフィックのみを活用するのでしょうか?
ATA はパケット精査テクノロジを使用して Active Directory を分析するほか、Security Information and Event Management (SIEM) から関連するイベントを収集し、Active Directory ドメイン サービスからの情報に基づいてエンティティのプロファイルを作成します。 また、組織が Windows イベント ログの転送を構成した場合、ATA はイベント ログからイベントを収集することもできます。

## ポート ミラーリングとは何ですか?
ポート ミラーリングは SPAN (スイッチ ポート アナライザー) とも呼ばれ、ネットワーク トラフィックの監視手法の 1 つです。 ポート ミラーリングを有効にすると、スイッチによって 1 つのポート (または全 VLAN) に見られるすべてのネットワーク パケットのコピーが別のポートに送信され、パケットはそこで分析されます。

## ATA はドメインに参加しているデバイスのみを監視するのでしょうか?
いいえ。 ATA は Active Directory に対して認証および承認要求を実行するネットワーク上のすべてのデバイス (Windows 以外のデバイスやモバイル デバイスを含む) を監視します。

## ATA はユーザー アカウント以外にコンピューター アカウントも監視しますか?
はい。 コンピューター アカウント (およびその他のエンティティ) を使用して悪意のあるアクティビティが実行される可能性もあるため、ATA はコンピューター アカウントや環境内のすべてのエンティティの行動を監視します。

## ATA は複数のドメインおよび複数のフォレストをサポートしますか?
一般公開リリースの Microsoft Advanced Threat Analytics では、同じフォレスト境界の複数のドメインがサポートされています。 フォレスト自体が実際の「セキュリティ境界」であるため、複数のドメインをサポートすることでお客様の環境の 100% を ATA でカバーできます。

## 展開の全体的な正常性を確認できますか?
はい、展開の全体的な正常性のほか、構成や接続などに関連する具体的な問題を確認できます。また、問題が発生するたびにアラートが発生します。


## 関連項目
- [ATA の前提条件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量計画](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [イベント コレクションの構成](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows イベント転送を構成する](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO3-->


