---
# required metadata

title: ATA アーキテクチャ | Microsoft Advanced Threat Analytics
description: Microsoft Advanced Threat Analytics (ATA) のアーキテクチャについて説明します
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA アーキテクチャ
Advanced Threat Analytics アーキテクチャの詳細をこのダイアグラムに示します。

![ATA アーキテクチャのトポロジ ダイアグラム](media/ATA-architecture-topology.jpg)

ATA は、物理スイッチまたは仮想スイッチを使用して ATA ゲートウェイにポート ミラーリングを行うか、または ATA Lightweight Gateway をドメイン コントローラー上に直接展開 (この場合、ポート ミラーリングは不要です) することにより、ドメイン コントローラーのネットワーク トラフィックを監視します。 さらに、ATA は Windows イベント (ドメイン コントローラーから直接か、または SIEM サーバーから転送されます) を活用し、攻撃と脅威のデータを分析することができます。
このセクションでは、ネットワークおよびイベント キャプチャのフローについて説明します。その後、ATA の主要なコンポーネントである、ATA ゲートウェイ、ATA Lightweight Gateway (コア機能は ATA ゲートウェイと同じです)、および ATA センターの機能について掘り下げて説明します。


![ATA トラフィック フローのダイアグラム](media/ATA-traffic-flow.jpg)

## ATA コンポーネント
ATA は、次の要素から構成されます。

-   **ATA センター** <br>
ATA センターは、展開している ATA ゲートウェイまたは ATA Lightweight Gateway (あるいはその両方) からデータを受信します。
-   **ATA ゲートウェイ**<br>
ATA ゲートウェイは、ドメイン コントローラーから発信されるトラフィックをポート ミラーリングまたはネットワーク タップのいずれかを使用して監視する、専用のサーバーにインストールされます。
-   **ATA Lightweight Gateway**<br>
ATA Lightweight Gateway は、ドメイン コントローラーに直接インストールされ、そのトラフィックを直接監視します。専用のサーバー、またはポート ミラーリングの構成は必要ありません。 これは、ATA ゲートウェイの代替となるものです。

ATA 展開は、ゲートウェイに接続された単一の ATA センターで構成できます。接続するゲートウェイの内訳は、すべて ATA ゲートウェイ、すべて ATA Lightweight Gateway、または ATA ゲートウェイおよび ATA Lightweight Gateway の組み合わせとすることができます。


## 展開オプション
ATA は、次のようにゲートウェイを組み合わせて使用し、展開することができます。

-   **ATA ゲートウェイのみを使用** <br>
ATA 展開に ATA Lightweight Gateway が含まれず、ATA ゲートウェイのみが含まれる場合、すべてのドメイン コントローラーで ATA ゲートウェイへのポート ミラーリングが有効になるように構成するか、またはネットワーク タップを設置する必要があります。
-   **ATA Lightweight Gateway のみを使用**<br>
ATA 展開に ATA Lightweight Gateway のみが含まれている場合、ATA Lightweight Gateway が各ドメイン コントローラーに展開されていることが必要です。追加のサーバー、またはポート ミラーリングの構成は必要ありません。
-   **ATA ゲートウェイおよび ATA Lightweight Gateway の両方を使用**<br>
ATA 展開に ATA ゲートウェイおよび ATA Lightweight Gateway の両方が含まれており、ATA Lightweight Gateway が一部のドメイン コントローラー (たとえば、ブランチ サイトのすべてのドメイン コントローラー) にインストールされ、その他のドメイン コントローラー (たとえば、メイン データ センターの大規模なドメイン コントローラー) が ATA ゲートウェイで監視されている場合です。

3 つのシナリオすべてで、すべてのゲートウェイは ATA センターにデータを送信します。




## ATA センター
**ATA センター**には、次の機能が備わっています。

-   ATA ゲートウェイおよび ATA Lightweight Gateway の構成設定を管理する

-   ATA ゲートウェイおよび ATA Lightweight Gateway からデータを受信する 

-   疑わしいアクティビティを検出する

-   異常な動作を検出するために、ATA で動作の機械学習アルゴリズムを実行する

-   攻撃 Kill Chain に基づいた高度な攻撃を検出するために、さまざまな決定論的アルゴリズムを実行する

-   ATA コンソールを実行する

-   省略可能: ATA センターは疑わしいアクティビティが検出されたときに電子メールやイベントを送信するように構成できます。

ATA センターは、ATA ゲートウェイおよび ATA Lightweight Gateway から解析されたトラフィックを受け取ってプロファイリングを行い、決定論的検出を実行し、機械学習と動作のアルゴリズムによりネットワークについて学習することで、異常を検出できるようにして疑わしいアクティビティについて警告します。

|||
|-|-|
|エンティティ レシーバー|すべての ATA ゲートウェイおよび ATA Lightweight Gateway からエンティティのバッチを受け取ります。|
|ネットワーク アクティビティ プロセッサ|受け取った各バッチ内のすべてのネットワーク アクティビティを処理します。 たとえば、別のコンピューターで実行された可能性のある各種 Kerberos 手順の間で照合します。|
|エンティティ プロファイラー|トラフィックとイベントに従って一意のすべてのエンティティをプロファイルします。 たとえば、これは ATA が各ユーザー プロファイルのログオンしているコンピューターのリストを更新する場所です。|
|センターのデータベース|ネットワーク アクティビティとイベントのデータベースへの書き込み処理を管理します。 |
|データベース|ATA は MongoDB を活用してシステム内の次のすべてのデータを格納します。<br /><br />-   ネットワーク アクティビティ<br />-   イベントのアクティビティ<br />-   一意のエンティティ<br />-   疑わしいアクティビティ<br />-   ATA 構成|
|検出部|検出部では、機械学習アルゴリズムと決定論的規則を使用して、ネットワーク内の疑わしいアクティビティやユーザーの異常行動を見つけます。|
|ATA コンソール|ATA コンソールは、ATA を構成し、ATA により検出されるネットワーク上の疑わしいアクティビティを監視します。 ATA コンソールは ATA センターのサービスに依存しないため、サービスが停止している場合でもデータベースと通信できる限りは実行されます。|
ネットワーク上に展開する ATA センターの数を決定する際には、次の要素を考慮してください。

-   1 つの ATA センターは、単一の Active Directory フォレストを監視できます。 1 つ以上の Active Directory フォレストがある場合は、Active Directory フォレストごとに 1 つ以上の ATA センターが必要です。

-    展開されている Active Directory の規模が非常に大きい場合、単一の ATA センターではすべてのドメイン コントローラーのすべてのトラフィックを処理できない可能性があります。 この場合は複数の ATA センターが必要になります。 ATA センターの数は、[ATA 容量計画](ata-capacity-planning.md)で指定することをお勧めします。.

## ATA ゲートウェイおよび ATA Lightweight Gateway

### ゲートウェイのコア機能
**ATA ゲートウェイ** および **ATA Lightweight Gateway** のコア機能は、両方とも同じです。

-   ドメイン コントローラーのネットワーク トラフィック (ATA ゲートウェイの場合はポート ミラーリングされたトラフィック、ATA Lightweight Gateway の場合はドメイン コントローラーのローカルのトラフィック) をキャプチャして検査する 

-   SIEM または Syslog サーバーから、または Windows イベント転送を使用してドメイン コントローラーから Windows イベントを受け取る

-   Active Directory ドメインからユーザーやコンピューターに関するデータを受け取る

-   ネットワーク エンティティ (ユーザー、グループ、コンピューター) の解決を実行する

-   関連データを ATA センターに転送する

-   1 つの ATA ゲートウェイにより複数のドメイン コントローラーを監視するか、または 1 つの ATA Lightweight Gateway により 1 つ のドメイン コントローラーを監視する

ATA ゲートウェイは、ネットワークからネットワーク トラフィックと Windows イベントを受け取り、次の主要なコンポーネントで処理します。

|||
|-|-|
|ネットワーク リスナー|ネットワーク リスナーは、ネットワーク トラフィックをキャプチャしてトラフィックを解析します。 このタスクは CPU の負荷が高いため、ATA ゲートウェイまたは ATA Lightweight Gateway を計画する際には [ATA の前提条件](ata-prerequisites.md)を確認してください。|
|イベント リスナー|イベント リスナーは、ネットワーク上の SIEM サーバーから転送される Windows イベントをキャプチャして解析します。|
|Windows イベント ログ リーダー|Windows イベント ログ リーダーは、ドメイン コントローラーから ATA ゲートウェイの Windows イベント ログに転送される Windows イベントを読み取って解析します。|
|ネットワーク アクティビティ トランスレータ | 解析されたトラフィックを、ATA で使用される、トラフィックの論理表現 (NetworkActivity) に変換します。
|エンティティ リゾルバー|エンティティ リゾルバーは、解析されたデータ (ネットワーク トラフィックとイベント) を取得し、Active Directory でデータを解決してアカウントと ID 情報を探し、 解析したデータで見つかった IP アドレスと照合します。 エンティティ リゾルバーは、パケット ヘッダーを効率的に検査し、コンピューター名、プロパティ、ID の認証パケットを解析できるようにして、 解析した認証パケットを実際のパケット内のデータに結合します。|
|エンティティ センダー|エンティティ センダーは、解析および照合されたデータを ATA センターに送信します。|

## ATA Lightweight Gateway の機能

次の機能は、ATA ゲートウェイまたは ATA Lightweight Gateway のどちらを実行しているかによって動作が異なります。

-   **ドメイン シンクロナイザー候補**<br>
ドメイン シンクロナイザー ゲートウェイは、特定の Active Directory ドメインのすべてのエンティティを事前対応的に同期します (ドメイン コント ローラー自体のレプリケーションで使用されるメカニズムに似ています)。 ドメイン シンクロナイザーとして機能する 1 つのゲートウェイが、候補の一覧からランダムに選択されます。 <br><br>
シンクロナイザーが 30 分を超えてオフラインの場合は、代わりに別の候補が選択されます。 特定のドメインに対して使用可能なドメイン シンクロナイザーがない場合、ATA はエンティティとその変更を事前対応的に同期することができませんが、監視対象のトラフィックで新しいエンティティが検出されると、ATA はそのエンティティを事後対応的に取得します。 
<br>使用可能なドメイン シンクロナイザーがなく、関連するトラフィックがなかったエンティティを検索した場合、検索結果は表示されません。<br><br>
既定では、すべての ATA ゲートウェイがシンクロナイザー候補です。<br><br>
すべての ATA Lightweight Gateway は、ブランチ サイトや小規模のドメイン コントローラーに配置される可能性の方が高いため、既定ではシンクロナイザー候補となっていません。


-   **リソースの制限事項**<br>
ATA Lightweight Gateway には、ゲートウェイが実行されているドメイン コントローラーで使用可能なコンピューティング能力とメモリ容量を評価する監視コンポーネントが含まれます。 監視プロセスは 10 秒ごとに実行され、ATA Lightweight Gateway プロセスの CPU 使用率およびメモリ使用率のクォータが動的に更新されます。これにより、どの時点においても、ドメイン コントローラーで使用可能な空きコンピューティング リソースおよび空きメモリ リソースを 15% 以上確保します。<br><br>
このプロセスでは、ドメイン コントローラーで何が起きてもそのコア機能に影響を与えないようにするため、リソースを常に解放します。<br><br>
これにより ATA Lightweight Gateway で使用可能なリソースがなくなった場合は、一部のトラフィックのみが監視され、監視アラート「ポート ミラーリングされたネットワーク トラフィックがドロップされました」が [正常性] ページに表示されます。

次の表に、使用可能なコンピューティング リソースが十分であり、クォータを現在必要な値より大きくすることができ、すべてのトラフィックが監視されるドメイン コントローラーの例を示します。

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|その他 (その他のプロセス) |ATA Lightweight Gateway のクォータ|ゲートウェイのドロップ|
|30%|20%|10%|45%|×|

Active Directory でより多くのコンピューティングが必要な場合は、ATA Lightweight Gateway で必要なクォータが減少します。 次の例では、ATA Lightweight Gateway は割り当て済みの値よりも多くのクォータを必要とし、一部のトラフィックがドロップされます (一部のトラフィックのみが監視されます)。

||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|その他 (その他のプロセス) |ATA Lightweight Gateway のクォータ|ゲートウェイのドロップ|
|60%|15%|10%|15%|○|



## お使いのネットワーク コンポーネント
ATA を操作する場合は、次のことを確認してください。

### ポート ミラーリング
ATA ゲートウェイを使用している場合は、監視対象のドメイン コントローラーのポート ミラーリングをセットアップし、物理スイッチまたは仮想スイッチを使用して ATA ゲートウェイを転送先に設定する必要があります。 別のオプションは、ネットワーク タップの使用です。 一部のドメイン コントローラーが監視されていない場合でも ATA は動作しますが、検出の効果は下がります。

ポート ミラーリングにより、ATA ゲートウェイへのドメイン コントローラーのすべてのトラフィックがミラーリングされますが、分析のために ATA センターに圧縮送信されるトラフィックはその中のほんの一部です。

ドメイン コントローラーと ATA ゲートウェイは物理または仮想のいずれでもかまいません。詳細については、「[Configure port mirroring (ポート ミラーリングの構成)](/advanced-threat-analytics/deploy-use/configure-port-mirroring)」を参照してください。


### イベント
Pass-the-Hash、ブルート フォース、およびハニー トークンの ATA 検出を強化するため、ATA は Windows イベント ログ ID 4776 を必要とします。 これは、ATA ゲートウェイが SIEM イベントをリッスンするように構成するか、または Windows イベント転送を使用することによって、ATA ゲートウェイに転送することができます。

-   SIEM イベントをリッスンするように ATA ゲートウェイを構成する <br>ATA に特定の Windows イベントを転送するように SIEM を構成します。 ATA には、多くの SIEM ベンダーがサポートされています。 詳細については、「[Configure event collection (イベント コレクションの構成)](/advanced-threat-analytics/deploy-use/configure-event-collection)」を参照してください。.

-   Windows イベント転送を構成する<br>ATA がイベントを取得するもう 1 つの方法は、Windows イベント 4776 を ATA ゲートウェイに転送するようにドメイン コントローラーを構成することです。 これは、SIEM を持っていない場合、または SIEM が ATA で現在サポートされていない場合に特に便利です。 ATA での Windows イベント転送の詳細については、「[Configuring Windows event forwarding (Windows イベント転送を構成する)](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)」を参照してください。.

## 関連項目
- [ATA の前提条件](ata-prerequisites.md)
- [ATA 容量計画](ata-capacity-planning.md)
- [イベント コレクションの構成](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows イベント転送を構成する](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA フォーラムを確認してください。](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO2-->


