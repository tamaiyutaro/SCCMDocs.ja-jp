---
title: "クラウド管理ゲートウェイの計画 | Microsoft Docs"
description: 
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: a7380ae781447880ffcba0778694ea62e10c4889
ms.contentlocale: ja-jp
ms.lasthandoff: 06/08/2017

---

# Configuration Manager でクラウド管理ゲートウェイを計画する
<a id="plan-for-the-cloud-management-gateway-in-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

バージョン 1610 より、クラウド管理ゲートウェイは、インターネット上で Configuration Manager クライアントを管理する簡単な方法を提供します。 クラウド管理ゲートウェイ サービスは、Microsoft Azure に展開され、Azure サブスクリプションを必要とします。 このサービスは、クラウド管理ゲートウェイ コネクタ ポイントと呼ばれる新しいロールを使って、オンプレミスの Configuration Manager インフラストラクチャに接続します。 デプロイされて構成されると、クライアントは、内部のプライベート ネットワーク上にいるかどうか、またはインターネット上にあるかどうかに関係なく、オンプレミスの Configuration Manager サイト システムの役割にアクセスできるようになります。

> [!TIP]  
> バージョン 1610 で導入されたクラウド管理ゲートウェイはプレリリース機能です。 有効にするには、「[更新プログラムからのプレリリース機能の使用](/sccm/core/servers/manage/pre-release-features)」をご覧ください。

Configuration Manager コンソールを使って、Azure にサービスを展開し、クラウド管理ゲートウェイ コネクタ ポイントの役割を追加して、クラウド管理ゲートウェイ トラフィックを許可するサイト システムの役割を構成します。 クラウド管理ゲートウェイは現在、管理ポイントとソフトウェアの更新ポイントの役割のみをサポートしています。

コンピューターを認証し、異なる層のサービス間の通信を暗号化するには、クライアント証明書および Secure Socket Layer (SSL) 証明書が必要です。 クライアント コンピューターは通常、グループ ポリシーの適用を介してクライアント証明書を受け取ります。 クライアントと役割をホストしているサイト システム サーバー間のトラフィックを暗号化するには、CA からカスタム SSL 証明書を作成する必要があります。 クラウド管理ゲートウェイ サービスの展開を Configuration Manager に許可する管理証明書を Azure で設定する必要もあります。

## クラウド管理ゲートウェイの要件
<a id="requirements-for-cloud-management-gateway" class="xliff"></a>

-   クライアント コンピューターとクラウド管理ゲートウェイ コネクタ ポイントを実行するサイト システム サーバー

-   クライアント コンピューターからの通信を暗号化し、クラウド管理ゲートウェイ サービスの ID を認証するために使用される内部 CA からのカスタムの SSL 証明書

-   クラウド サービスの Azure サブスクリプション

-   Azure での Configuration Manager の認証に使用される Azure 管理証明書

## クラウド管理ゲートウェイの仕様
<a id="specifications-for-cloud-management-gateway" class="xliff"></a>

- クラウド管理ゲートウェイの各インスタンスは、4,000 クライアントをサポートします。
- 可用性を高めるため、クラウド管理ゲートウェイのインスタンスを少なくとも 2 つ作成することをお勧めします。
- クラウド管理ゲートウェイは、管理ポイントとソフトウェアの更新ポイントの役割のみをサポートしています。
-   クラウド管理ゲートウェイに関しては、Configuration Manager の次の機能が現在のところサポートされていません。

    -   クライアント展開
    -   サイトの自動割り当て
    -   ユーザー ポリシー
    -   アプリケーション カタログ (ソフトウェア承認要求を含む)
    -   完全なオペレーティング システム展開 (OSD)
    -   Configuration Manager コンソール
    -   ［リモート ツール］
    -   Web サイトのレポート
    -   Wake On LAN
    -   Mac、Linux、UNIX クライアント
    -   Azure Resource Manager
    -   ピア キャッシュ
    -   オンプレミス モバイル デバイス管理

## クラウド管理ゲートウェイのコスト
<a id="cost-of-cloud-management-gateway" class="xliff"></a>

>[!IMPORTANT]
>以下のコスト情報は、見積もり目的のみで提供されます。 ご利用の環境によっては、変動要素が他にも存在し、それがクラウド管理ゲートウェイの総コストに影響を与えることがあります。

クラウド管理ゲートウェイでは、次の Microsoft Azure の機能が使用され、その料金が Azure サブスクリプション アカウントに請求されます。

-   バーチャル マシン

    -   現在のところ、クラウド管理ゲートウェイには Standard\_A2 バーチャル マシンが必要になります。 サービスを作成するとき、サービスをサポートする VM の数を選択できます (既定は 1 です)。

    -   1 台の Azure Standard\_A2 バーチャル マシンでインターネット ベースのクライアントを約 2,000 台同時にサポートできると予想されます (この数値は見積もり目的でのみ提供されます)。

    -   予想されるコストについては、「[Azure の料金計算ツール](https://azure.microsoft.com/en-us/pricing/calculator/)」を参照してください。

      >[!NOTE]
      >バーチャル マシンのコストは地域によって異なります。

-   送信データの転送

    -   サービスから送信されるデータに対して料金が発生します。 予想されるコストについては、「[Azure 帯域幅の料金詳細](https://azure.microsoft.com/en-us/pricing/details/bandwidth/)」を参照してください。

    -   インターネット ベースのクライアントが 1 時間ごとにポリシーを更新する場合、クライアントあたり毎月約 100 MB が予想されます (この数値は見積もり目的でのみ提供されます)。

    >[!NOTE]
    > クラウド管理ゲートウェイでサポートされている他のアクションを実行すると (ソフトウェアの更新プログラムやアプリケーションの展開など)、Azure から送信されるデータが増えます。

-   コンテンツ ストレージ

    -   クラウド管理ゲートウェイで管理されるインターネット ベースのクライアントは、Windows Update から無料でソフトウェア更新プログラム コンテンツを受信します。

    -   その他の必要なコンテンツ (アプリケーションなど) は、クラウド ベースの配布ポイントに配布する必要があります。 現在のところ、クラウド管理ゲートウェイでは、コンテンツをクライアントに送信するときにのみ、クラウド配布ポイントがサポートされます。

    - 詳細については、「[クラウドベースの配布にかかるコスト](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution)」を参照してください。

## クラウド管理ゲートウェイ (CMG) についてよく寄せられる質問
<a id="frequently-asked-questions-about-the-cloud-management-gateway-cmg" class="xliff"></a>

### なぜクラウド管理ゲートウェイを使用するのですか?
<a id="why-use-the-cloud-management-gateway" class="xliff"></a>

このロールを使用することで、インターネット ベースのクライアント管理が、Configuration Manager コンソールから 3 つの手順で簡単に行えるようになります。

1. [クラウド管理ゲートウェイの作成](/sccm/core/clients/manage/setup-cloud-management-gateway)ウィザードを使用して、CMG を Azure にデプロイします。
2. [クラウド管理ゲートウェイ接続ポイント](/sccm/core/servers/deploy/configure/install-site-system-roles)のサイト システム ロールを構成します。
3. [クラウド管理ゲートウェイ トラフィック](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic)のロールを構成します (管理ポイント、ソフトウェアの更新ポイントなど)。

### クラウド管理ゲートウェイはどのような仕組みになっていますか?
<a id="how-does-the-cloud-management-gateway-work" class="xliff"></a>

- クラウド管理ゲートウェイ接続ポイントは、インターネットからクラウド管理ゲートウェイへの一貫性のある高パフォーマンスな接続を可能にします。
- Configuration Manager は、接続情報やセキュリティ設定などの各種設定を CMG に発行します。
- CMG は、Configuration Manager クライアントの要求を認証し、クラウド管理ゲートウェイ接続ポイントに転送します。 これらの要求は、URL マッピングに従って企業ネットワーク内のロールに転送されます。

### クラウド管理ゲートウェイのデプロイはどうやって行いますか?
<a id="how-is-the-cloud-management-gateway-deployed" class="xliff"></a>

CMG のデプロイ タスクはすべて、サービス接続ポイントのクラウド サービス マネージャー コンポーネントによって処理されます。 また、このコンポーネントは、Azure AD のサービスの正常性とログ情報も監視し、レポートします。

#### 証明書の要件
<a id="certificate-requirements" class="xliff"></a>

CMG のセキュリティ保護には、次の証明書が必要になります。

- **管理証明書** - 自己署名証明書を含む、任意の証明書を使用できます。 Azure AD にアップロードされた公開証明書、または Azure AD での認証用に Configuration Manager にインポートされた[秘密キー付きの PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) を使用できます。
- **Web サービス証明書** -  クライアントによるネイティブな信頼を得るために、パブリック CA 証明書を使用することをお勧めします。 CNAME は、パブリック DNS レジスタで作成する必要があります。 ワイルド カード証明書はサポートされていません。
- **CMG にアップロードされたルート証明書または SubCA 証明書** - クライアントの PKI 証明書に対して、CMG がチェーンの完全検証を行う必要があります。 クライアント PKI 証明書の発行に エンタープライズ CA を使用していて、証明書のルート CA や下位 CA がインターネットにない場合は、エンタープライズ CA を CMG にアップロードする必要があります。

#### デプロイのプロセス
<a id="deployment-process" class="xliff"></a>

デプロイには次の 2 つのフェーズがあります。

- クラウド サービスのデプロイ
    - [Azure サービス定義スキーマ](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef) ファイルをアップロードする
    - [Azure サービス構成スキーマ](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg) ファイルをアップロードする。
- Azure AD サーバーでの CMG コンポーネントのセットアップと、エンドポイント、HTTP ハンドラー、インターネット インフォメーション サービス (IIS) のサービスの構成

CMG の構成を変更する場合は、構成のデプロイが CMG に行われます。

### クラウド管理ゲートウェイは、どうやってセキュリティを確実にするのですか?
<a id="how-does-the-cloud-management-gateway-help-ensure-security" class="xliff"></a>

CMG は次の方法で、セキュリティによる保護を確実なものにします。

- 内部証明書と接続 ID を使用して、相互 SSL 認証を含む CMG 接続からの接続を承諾し、管理します。
- クライアント要求の承諾と転送
    - クライアント PKI 証明書の 相互 SSL を使用して、接続を事前に認証します。
    - 証明書信頼リストが、クライアント PKI 証明書のルートを確認します。 この設定は、サイトのプロパティのクライアント通信設定で指定できます。 またクライアントに対して、管理ポイントと同じ検証を実施します。
    - 受信した URL を確認します。
    - 受信した URL をフィルターして、接続している CMG 接続ポイントのなかで URL 要求を処理できるものがないか確認します。  
    - 発行エンドポイントごとにコンテンツの長さのチェックを確認します。
    - 「ラウンドロビン」を使用して、同一サイトからの CMG 接続ポイント間の負荷を分散します。

- CMG 接続ポイントの保護
    - 接続している CMG のすべての仮想インスタンスに対して、一貫性のある HTTP/TCP 接続を構築します。 1 分ごとに接続を確認し、維持します。
    - 内部証明書を使用する CMG で、SSL 認証を相互に認証します。
    - URL マッピングに基づいて、HTTP 要求を転送します。
    - 接続の状態をレポートして管理サービスの正常性状態を表示します。
    - エンドポイント別のエンドポイントのトラフィックレポートを、5 分ごとにレポートします。

- 管理ポイントのようなロールと向き合っている発行エンドポイント Configuration Manager クライアントと、IIS のソフトウェアの更新ポイント ホスト エンドポイントをセキュリティで保護してクライアントの要求を処理します。 CMG に発行されたすべてのエンドポイントに、URL マッピングがあります。
外部 URL は、CMG との通信にクライアントが使用する URL です。
内部 URL は、内部サーバーに要求を転送するときに使用する CMG 接続ポイントです。

#### 例:
<a id="example" class="xliff"></a>
管理ポイントの CMG トラフィックを有効にすると、ccm_system、ccm_incoming、sms_mp などの 各管理ポイント サーバーの URL マッピングのセットが、Configuration Manager 内で作成されます。
管理ポイントの ccm_system のエンドポイントの外部 URL は、**https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System** のようになります。
この URL は、管理ポイントごとに一意となっています。 その後、Configuration Manager クライアントによって、**<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>** のような CMG が有効化された MP 名がインターネット管理ポイントのリストに追加されます。
発行された外部 URL はすべて自動で CMG にアップロードされます。その後、CMG による URL のフィルタリングが可能になります。 すべての URL マッピングは、外部 URL を要求するクライアントに応じて内部サーバーに転送できるように、CMG 接続ポイントに複製されます。

### クラウド管理ゲートウェイが使用するポートは何ですか?
<a id="what-ports-are-used-by-the-cloud-management-gateway" class="xliff"></a>

- オンプレミスのネットワークでは、受信ポートは必要ありません。 CMG をデプロイすると、CMG 上に自動的に作成されます。
- 443 以外の一部の送信ポートは、CMG 接続ポイントで必要です。

|||||
|-|-|-|-|
|データ フロー|サーバー|サーバーのポート|クライアント|
|CMG のデプロイ|Azure|443|Configuration Manager サービス接続ポイント|
|CMG チャネルの構築|CMG|VM インスタンス: 1 個のポート: 443<br>VM インスタンス: N (N > = 2、N < = 16) 個のポート: 10124 ~ N 10140 ~ N|CMG 接続ポイント|
|クライアントから CMG|CMG|443|クライアント|
|CMG コネクタからサイトの役割 (現状、管理ポイントとソフトウェアの更新ポイント)|サイトの役割|サイトの役割で構成されているプロトコル/ポート|CMG 接続ポイント|

### クラウド管理ゲートウェイのパフォーマンスを強化する方法はありますか?
<a id="how-can-you-improve-performance-of-the-cloud-management-gateway" class="xliff"></a>

- 可能な場合、CMG、CMG 接続ポイント、Configuration Manager のサイト サーバーは同じネットワーク リージョンで構成してください。待機時間を減らすことができます。
- 現在、Configuration Manager クライアントと CMG 間の接続は、リージョンを意識していません。
- 高可用性を得るために、1 サイトあたり少なくとも 2 つの CMG 仮想インスタンスと 2 つの CMG 接続ポイントをお勧めします。
- VM インスタンスを追加することで CMG をスケールし、より多くのクライアントをサポートできます。 これらは、Azure AD のロード バランサーによって負荷分散されています。
- CMG 接続ポイントを増やすことで、ポイント間の負荷を分散できます。 CMG は接続している CMG 接続ポイントに対して、トラフィックを「ラウンドロビン」で処理します。
- 1702 のリリースでサポートされているクライアントの数は、CMG VM インスタンスあたり 6,000 台です。 CMG チャネルが高負荷状態のときでも要求は処理されますが、通常よりも時間がかかる場合があります。

### クラウド管理ゲートウェイを監視する方法はありますか?
<a id="how-can-you-monitor-the-cloud-management-gateway" class="xliff"></a>

デプロイのトラブルシューティングの場合は、**CloudMgr.log** と **CMGSetup.log** を使用します。
サービス正常性のトラブルシューティングの場合は、**CMGService.log** と **SMS_CLOUD_PROXYCONNECTOR.log** を使用します。
クライアントのトラフィックのトラブルシューティングの場合は、**CMGHttpHandler.log**、**CMGService.Log**、**SMS_CLOUD_PROXYCONNECTOR.log** を使用します。

CMG 関連のすべてのログ ファイルの一覧は、[Configuration Manager のログ ファイル](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)に関するページをご覧ください。

## 次のステップ
<a id="next-steps" class="xliff"></a>

[Set up cloud management gateway](setup-cloud-management-gateway.md) (クラウド管理ゲートウェイの設定)

