---
title: "境界グループの定義 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントとサイト システムをつなげる境界グループを理解します。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d940fd1bbf96767d44f8c55315e814be55a83897
ms.openlocfilehash: 5684fd4fbfd0ffb8f3ffbcfa122eef3dafd77327
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017


---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>System Center Configuration Manager の境界グループを構成する


*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の境界グループを利用し、関連するネットワークの場所 ([境界](/sccm/core/servers/deploy/configure/boundaries)) を論理的にグループ化し、インフラストラクチャの管理を簡単にします。 境界グループを使用するには、先に境界を境界グループに割り当てておく必要があります。

既定では、Configuration Manager は各サイトで既定のサイト境界グループを作成します。

> [!IMPORTANT]  
>  **この「境界グループ」セクションと子セクションの情報は、バージョン 1610 以降に適用されます。** このドキュメントの内容は、この更新プログラム バージョンで境界グループに導入された設計の変更に従って改訂されました。
>
> **使用しているバージョンが 1610 より前の場合**に境界グループを使用および構成する方法については、「[Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)」(System Center Configuration Manager バージョン 1511、1602、1606 の境界グループ) を参照してください。

境界グループを構成するには、境界 (ネットワークの場所) とサイト システムの役割を、配布ポイントのように、境界グループに関連付けます。 これは、ネットワーク上のクライアントの近くにある配布ポイントのようにサイト システム サーバーにクライアントを関連付けることに役立ちます。

同じ境界を複数の境界グループに割り当て、同じサイト システム サーバーを配布ポイントのように複数の境界グループに割り当てるには、サイト システムの可用性を広範囲のネットワークの場所まで増やします。

クライアントは、次の目的で境界グループを使用します。  

-   サイトの自動割り当て  
-   サービスを提供できるサイト システム サーバーを見つけるため (次を含む):
    - コンテンツの場所の配布ポイント
    -    ソフトウェア更新ポイント (バージョン 1702 より)
    - 状態移行ポイント
    - 優先管理ポイント (優先管理ポイントを使用する場合は、境界グループの構成内からではなく、階層に対してこのオプションを有効にする必要があります。 このトピックの「[優先管理ポイントの使用を有効にする](#to-enable-use-of-preferred-management-points)」を参照してください。)

##  <a name="boundary-groups-and-relationships"></a>境界グループとリレーションシップ
階層の境界グループごとに、次を割り当てることができます。

-  1 つまたは複数の境界。 特定の境界グループに割り当てられている境界として定義されているネットワークの場所にクライアントが置かれているとき、それは**現在**の境界グループと呼ばれます。 クライアントには複数の現在の境界グループを設定できます。
- 1 つまたは複数のサイト システムの役割。  クライアントは常に、現在の境界グループに関連付けられているサイト システムの役割を使用できます。 追加の構成によっては、追加の境界グループのサイト システムの役割を使用できることがあります。  

作成する境界グループごとに、別の境界グループへの一方向リンクを構成できます。 そのリンクは**リレーションシップ**と呼ばれます。 リンク先の境界グループは**近隣**境界グループと呼ばれます。 境界グループには複数のリレーションシップを設定できます。各リレーションシップに特定の近隣境界グループが与えられます。

クライアントはその現在の境界グループで利用できるサイト システム サーバーが見つからないと、近隣境界グループを探して利用できるサイト システムを見つけますが、その検索開始のタイミングは各リレーションシップの構成により決定します。 この追加グループ検索は**フォールバック**と呼ばれます。

## <a name="fallback"></a>フォールバック
クライアントが現在の境界グループで利用できるサイト システムを見つけられない問題を回避するために、フォールバック動作を決定する境界グループ間のリレーションシップを定義します。 フォールバックを利用することで、クライアントはその検索範囲を追加の境界グループまで拡大し、利用できるサイト システムを見つけることができます。

リレーションシップは **[リレーションシップ]** タブの境界グループ プロパティで構成されます。 リレーションシップを構成するとき、近隣境界グループへのリンクを定義します。 サポートされるサイト システムの役割の種類ごとに、その近隣境界グループへのフォールバックの独立した設定を構成できます。 たとえば、ある境界グループに対するリレーションシップを構成するとき、既定の 120 分ではなく、20 分後に配布ポイントのフォールバックが発生するように設定できます。 他のさまざまな例については、「[境界グループの使用例](#example-of-using-boundary-groups)」を参照してください。

クライアントがその現在の境界グループで利用できるサイト システムの役割を見つけられない場合、そのクライアントは、フォールバック時間 (分) を利用し、その近隣境界グループに関連付けられている利用できるサイト システムの検索開始までの時間を決定します。  

クライアントが利用できるサイト システムを見つけられず、近隣境界グループから場所の検索を開始するとき、クライアントは利用できるサイト システムのプールを増やします。そのプールは、境界グループとそのリレーションシップの構成により定義される方法で利用できます。

- 境界グループには複数のリレーションシップを設定できます。 サイト システムの種類ごとにフォールバックを構成し、フォールバック開始までの時間に近隣ごとに別の値を設定できます。    
- クライアントは、現在の境界グループに直接隣接している境界グループにのみフォールバックします。
- クライアントが複数の境界グループのメンバーである場合は、現在の境界グループが、そのクライアントのすべての境界グループの結合として定義されます。 そのクライアントは元のいずれかの境界グループの近隣にフォールバックできます。

### <a name="the-default-site-boundary-group"></a>既定のサイト境界グループ
作成する境界グループ以外に、Configuration Manager により作成された既定のサイト境界グループが各サイトに与えられます。 このグループには ***Default-Site-Boundary-Group&lt;sitecode>*** という名前が付きます。 たとえば、サイト ABC のグループの名前は *Default-Site-Boundary-Group&lt;ABC>* になります。

作成する境界グループごとに、Configuration Manager は自動的に、階層の既定の各サイト境界グループに暗黙的リンクを作成します。
-    この暗黙的リンクは、現在の境界グループからサイトの既定の境界グループへの既定のフォールバック オプションです。既定の境界グループには、120 分という既定のフォールバック時間が設定されています。
-    階層内の境界グループに関連付けられている境界にないクライアントは、それに割り当てられているサイトの既定のサイト境界グループを利用し、それが利用できるサイト システムの役割を特定します。

既定のサイト境界グループへのフォールバックを管理するには:
- サイトの既定の境界グループのプロパティに進み、**[既定の動作]** タブの値を変更できます。 ここで行う変更は、この境界グループの*すべて*の暗黙的リンクに適用されます。 以上の設定は、別の境界グループからこの既定のサイト境界グループの明示的リンクを構成すると無視されます。
- 作成した境界グループのプロパティに移動し、既定のサイト境界グループに進む明示的リンクの値を変更できます。 フォールバックに新しい時間 (分) を設定したり、フォールバックをブロックしたりした場合、その変更はあなたが構成しているリンクにのみ影響を与えます。 明示的リンクの構成は、既定のサイト境界グループの **[既定の動作]** タブの構成より優先されます。


## <a name="site-assignment"></a>サイトの割り当て  
 各境界グループごとに、クライアント用の割り当てられたサイトを構成できます。  

-   サイトの自動割り当てを使用する新しくインストールされたクライアントは、クライアントの現在のネットワークの場所を含む境界グループの割り当て済みサイトに参加します。  
-   サイトに割り当てられると、クライアントがネットワークの場所を変更するときに、クライアントのサイトの割り当てが変更されることはありません。 たとえば、別のサイトが割り当てられた境界グループ内の境界が示されている新しいネットワークの場所にクライアントがローミングしたとしても、クライアントに対して割り当てられたサイトが変更されることはありません。  
-   Active Directory システムの探索で新しいリソースが検出されると、検出されたリソースのネットワーク情報が境界グループ内の境界に対して評価されます。 このプロセスにより、割り当てられたサイトに新しいリソースが関連付けられ、クライアント プッシュ インストール方法で使用できるようになります。  
-   境界が、異なる割り当て済みサイトを持つ複数の境界グループのメンバーである場合は、クライアントによってランダムにいずれかのサイトが選択されます。  
-   境界グループの割り当て済みサイトへの変更は、新しいサイトの割り当て操作にのみ適用されます。 以前にサイトに割り当て済みのクライアントは、境界グループの構成の変更 (またはクライアントのネットワークの場所の変更) に基づくサイトの割り当てを再評価しません。  

クライアントのサイトの割り当ての詳細については、「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../../core/clients/deploy/assign-clients-to-a-site.md)」の「[コンピューターにサイトの自動割り当てを使用する](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)」をご覧ください。  

## <a name="distribution-points"></a>配布ポイント

クライアントが配布ポイントの場所を要求すると、Configuration Manager はそのクライアントに、クライアントの現在のネットワークの場所を含む各境界グループに関連付けられている (適切な種類の) サイト システムの一覧を送信します。

-   **ソフトウェアの配布時**、クライアントは、配布ポイントまたはその他の有効なコンテンツ ソース (ピア キャッシュに構成されているクライアントなど) から利用できる展開コンテンツの場所を要求します。

-   **オペレーティング システムの展開時**に、クライアントは状態移行情報の送受信用の場所を要求します。  

コンテンツの展開中、現在の境界グループのソースから利用できないコンテンツをクライアントが要求した場合、そのクライアントは、近隣境界グループまたは既定のサイト境界グループのフォールバック時間に到達するまで、そのコンテンツの要求を続け、その現在の境界グループでさまざまなコンテンツ ソースを試します。 クライアントがコンテンツを見つけていない場合、コンテンツ ソースの検索範囲を拡大し、近隣境界グループを含めます。

ただし、コンテンツがオンデマンドで配布され、配布ポイントでは利用できない場合、クライアントが要求すると、その配布ポイントにコンテンツを転送するプロセスが開始します。フォールバックして近隣境界グループを使用する前にコンテンツ ソースとしてそのサーバーをクライアントが見つけることがありえます。

## <a name="software-update-points"></a>ソフトウェアの更新ポイント
バージョン 1702 以降では、クライアントは境界グループを利用し、新しいソフトウェア更新ポイントを検出します。 ソフトウェアの更新ポイントをそれぞれ異なる境界グループに追加して、クライアントで検索できるサーバーを制御できます。

1702 より前のバージョンから更新すると、すべての既存ソフトウェア更新ポイントが各サイトで既定のサイト境界グループに追加されます。 それにより、自分の階層に対して自分で構成した利用できるソフトウェア更新ポイント プールからクライアントがソフトウェア更新ポイントを選択するという更新以前の動作が維持されます。  この動作は、選択とフォールバックの動作が制御されている異なる境界グループに個々のソフトウェア更新ポイントを追加するまで維持されます。

バージョン 1702 以降を実行している新しいサイトをインストールする場合は、ソフトウェア更新ポイントを境界グループに割り当てる必要があります。その後、クライアントでこれを検索して使用できます。


ソフトウェア更新ポイントのフォールバックは他のサイト システムの役割と同様に構成されますが、次のような注意点があります。
- **新しいクライアントは境界グループを使用してソフトウェア更新ポイントを選択します。** バージョン 1702 をインストールすると、インストールした新しいクライアントは、構成した境界グループに関連付けられているものからソフトウェア更新ポイントを選択します。

  これは、クライアントがクライアント フォレストを共有するソフトウェア更新ポイントのリストからランダムに選択する以前の動作に取って代わるものです。

- **以前にインストールされたクライアントは、フォールバックして新しいソフトウェアの更新ポイントを見つけるまで、引き続き、現在のものを使用します。** 以前にインストールされ、既にソフトウェア更新ポイントがあるクライアントは、そのサーバーに到達できなくなるまで、そのソフトウェア更新ポイントを引き続き使用します。 クライアントの現在の境界グループに関連付けられていないソフトウェア更新ポイントも引き続き使用されます。

  ソフトウェア更新ポイントが既に与えられているクライアントがそれに到達できないとき、フォールバックして別のものを見つけることができます。 フォールバックを利用するとき、クライアントはその現在の境界グループからのソフトウェア更新ポイントの全一覧を受け取ります。 利用できるサーバーが 120 分で見つからなかった場合、近隣境界グループや既定のサイト境界グループにフォールバックします。 この 2 つの境界グループへのフォールバックは同時に行われます。ソフトウェア更新ポイントの近隣境界グループへのフォールバック時間が 120 分に設定されており、変更できないからです。 120 分は、既定のサイト境界グループへのフォールバックの規定時間でもあります。 クライアントが近隣境界グループと既定のサイト境界グループの両方にフォールバックするとき、クライアントは近隣境界グループからソフトウェア更新ポイントへの接触を試み、それから既定のサイト境界グループのソフトウェア更新ポイントの使用を試みます。

  そのサーバーがクライアントの現在の境界グループにないときでも、既存のソフトウェア更新ポイントが意図的に引き続き使用されます。 これは、ソフトウェアの更新ポイントが変更されると、クライアントがデータと新しいソフトウェアの更新ポイントを同期する場合に、ネットワーク帯域幅が多く使用される可能性があるためです。 遷移の遅延は、すべてのクライアントが新しいソフトウェアの更新ポイントに同時に切り替える場合に、ネットワークの飽和を回避するのに役立ちます。

- **フォールバック時間の構成:** 他のサイト システムの役割のフォールバック構成とは異なり、ソフトウェア更新ポイントは分単位の時間構成にまだ対応していません。 代わりに、フォールバック動作は以下に制限されています。  
  - **フォールバック時間 (分単位):** ソフトウェア更新ポイントに対してこのオプションは灰色表示になり、構成できません。 120 分に設定されています。
  -     **フォールバックしない:** この構成を使用すると、ソフトウェア更新ポイントのために近隣境界グループにフォールバックする動作をブロックできます。

## <a name="preferred-management-points"></a>優先管理ポイント

 優先管理ポイントを使用すると、クライアントは、その現在のネットワークの場所 (境界) に関連付けられた管理ポイントを特定できます。  

-   クライアントは、優先として構成されていない割り当て済みサイトからの管理ポイントを使用する前に、割り当て済みサイトからの優先管理ポイントを使用しようとします。  
-   このオプションを使用するには、それを階層に対して有効にして、境界グループの関連境界に関連付ける必要がある管理ポイントを含めるように個々のプライマリ サイトの境界グループを構成する必要があります。  
-   優先管理ポイントが構成され、クライアントが管理ポイントの一覧を整理するときに、割り当て済み管理ポイントの一覧 (クライアントの割り当て済みサイトからのすべての管理ポイントを含む) の一番上に優先管理ポイントがクライアントにより配置されます。  

> [!NOTE]  
>  クライアントのローミング時 (ラップトップ コンピューターをリモート オフィスに持って行くときなど、クライアントのネットワークの場所を変更するとき) に、クライアントは新しい場所でローカル サイトからの管理ポイント (またはプロキシ管理ポイント) を使用してから、割り当て済みサイト (優先管理ポイントがあるサイト) からの管理ポイントを使用する場合があります。  詳細については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」をご覧ください。  

### <a name="overlapping-boundaries"></a>重複する境界  
 Configuration Manager は、コンテンツの場所について、重複する境界を持つ構成をサポートします。  

-   **クライアントがコンテンツを要求し**、クライアントのネットワークの場所が複数の境界グループに属している場合、Configuration Manager はコンテンツが格納されているすべての配布ポイントのリストをクライアントに送信します。  
-   **クライアントが状態移行情報の送受信をサーバーに要求し**、クライアントのネットワークの場所が複数の境界グループに属している場合は、Configuration Manager は、クライアントの現在のネットワークの場所を含む境界グループに関連付けられた状態移行ポイントのリストをクライアントに送信します。  

この動作により、コンテンツまたは状態移行情報の転送元となる最も近いサーバーをクライアントが選択できるようになります。  



## <a name="example-of-using-boundary-groups"></a>境界グループの使用例
次の例では、クライアントは配布ポイントからコンテンツを探します。 この例は、境界グループを利用する他のサイト システムの役割にも適用できます。 ただし、ソフトウェア更新ポイントへの適用に関しては、ソフトウェア更新ポイントは近隣グループにフォールバックする時間 (分単位) を構成できず、常に 120 分という時間を使用することに留意してください。

境界またはサイト システム サーバーを共有しない次の 3 つの境界グループを作成します。
-    配布ポイント DP_A1 と DP_A2 が関連付けられたグループ BG_A
-    配布ポイント DP_B1 と DP_B2 が関連付けられたグループ BG_B
-    配布ポイント DP_C1 と DP_C2 が関連付けられたグループ BG_C

クライアントのネットワークの場所を境界として BG_A 境界グループにのみ追加し、その境界グループから他の 2 つの境界グループへのリレーションシップを構成します。
-    10 分後に使用する 1 つ目の*近隣*グループ (BG_B) に配布ポイントを構成します。 このグループには、配布ポイント DP_B1 と DP_B2 が含まれています。 どちらも、最初のグループの境界の場所に適切に接続されています。
-    20 分後に使用するように 2 つ目の*近隣*グループ (BG_C) を構成します。 このグループには、配布ポイント DP_C1 と DP_C2 が含まれています。 どちらも、他の 2 つの境界グループから WAN を経由します。
-    また、サイト サーバーに配置される追加の配布ポイントをサイトの既定のサイト境界グループに追加します。 これは、最小限の推奨されるコンテンツ ソースの場所ですが、すべての境界グループの中心的な場所に配置されます。

    境界グループとフォールバック時間の例:

     ![BG_Fallack](media/BG_Fallback.png)


この構成では:
-    クライアントは*現在の*境界グループ (BG_A) 内の配布ポイントからコンテンツの検索を開始し、各配布ポイントを 2 分間検索してから、境界グループ内の次の配布ポイントに切り替えます。 有効なコンテンツ ソースの場所のクライアントのプールには、DP_A1 と DP_A2 が含まれています。
-    クライアントは*現在の* 境界グループを 10 分間検索してコンテンツが見つからなかった場合、BG_B 境界グループから配布ポイントを検索に追加します。 BG_A と BG_B の両方の境界グループからの配布ポイントを含む結合された配布ポイントのプール内の配布ポイントからコンテンツの検索を続行します。 クライアントは引き続き各配布ポイントを 2 分間検索してから、そのプール内の次の配布ポイントに切り替えます。 有効なコンテンツ ソースの場所のクライアントのプールには、DP_A1、DP_A2、DP_B1、DP_B2 が含まれています。
-    さらに 10 分 (合計 20 分) 経っても、クライアントがコンテンツがある配付ポイントをまだ見つけられない場合は、利用可能な配布ポイントのプールを拡大して、2 番目の*近隣*グループ (境界グループ BG_C) からの配付ポイントを含めます。 これで、クライアントが検索する配布ポイントが 6 個 (DP_A1、DP_A2、DP_B2、DP_B2、DP_C1、DP_C2) になり、コンテンツが見つかるまで 2 分ごとに新しい配布ポイントへの切り替えを続行します。
-    合計で 120 分経ってもクライアントがコンテンツを見つけられない場合は、フォールバックして*既定サイトの境界グループ*を継続的な検索の一部として含めます。 これで配布ポイントのプールに構成した 3 つの境界グループからすべての配布ポイントが含まれ、最後の配布ポイントがサイト サーバー コンピューター上に配置されました。  クライアントはコンテンツが見つかるまで 2 分ごとに配布ポイントを切り替えてコンテンツの検索を続けます。

異なる時間に異なる近隣グループが利用可能になるように構成することで、特定の配布ポイントがコンテンツ ソースの場所として追加されるタイミング、およびクライアントが既定サイトの境界グループへのフォールバックを他の場所から使用できないコンテンツのセーフティ ネットとして使用するタイミングまたは状況を制御します。






### <a name="update-existing-boundary-groups-to-the-new-model"></a>既存の境界グループを新しいモデルに更新する
1610 より前のバージョンに更新すると、次の構成が自動的に設定されます。 これらは、新しい境界グループおよびリレーションシップを構成するまで、現在のフォールバック動作をそのまま利用できるようにすることを目的としています。

-    各プライマリ サイトに既定のサイト境界グループが作成されます。名前は ***Default-Site-Boundary-Group&lt;サイトコード>*** です。
  -    *[代替のコンテンツ ソースの場所の使用を許可する]* がオンの配布ポイントと、プライマリ サイトの状態移行ポイントは、そのサイトの *Default-Site-Boundary-Group&lt;サイトコード>* 境界グループに追加されます。
  -    バージョン 1702 以降、ソフトウェア更新ポイントは各サイト *Default-Site-Boundary-Group&lt;sitecode>* に追加されます。
-    低速接続が設定されているサイト サーバーを含む既存の各境界グループのコピーが作成されます。 新しいグループの名前は、***&lt;元の境界グループ名>-&lt;元の境界グループ ID>*** です。  
    -    高速接続が設定されているサイト システムは、元の境界グループに残されます。
    -    低速接続が設定されているサイト システム (配布ポイント、管理ポイント) のコピーは、境界グループのコピーに追加されます。 低速接続で設定されている元のサイト システムは、後方互換性のために元の境界グループに残っていますが、その境界グループからは使用されません。
    - この境界グループのコピーには、それに関連付けられている境界はありません。 ただし、元のグループとフォールバックの時間が 0 に設定された新しい境界グループのコピー間にフォールバック リンクが作成されます。  


- **セカンダリ サイトに固有:**
  - セカンダリ サイトに *[代替のコンテンツ ソースの場所の使用を許可する]* がオンの配布ポイント、または状態移行ポイントが少なくとも 1 つある場合、境界グループが作成されます。 境界グループの名前は、***Secondary-Site-Neighbor--Tmp&lt;サイトコード>*** です。
  - *[代替のコンテンツ ソースの場所の使用を許可する]* がオンのすべての配布ポイントと、状態移行ポイントは、この新しく作成されたセカンダリ サイト境界グループに追加されます。
  - 元の境界グループと新しく作成された近隣境界グループ間にフォールバック リンクが作成され、フォールバック時間が 0 に設定されます。


 次の表に、元の展開設定と配付ポイントの設定の組み合わせから期待できる新しいフォールバック動作を示します。

低速ネットワークでの [プログラムを実行しない] の元の展開構成  |[代替のコンテンツ ソースの場所の使用をクライアントに許可する] の元の配布ポイントの構成  |新しいフォールバック動作  
---------|---------|---------
オン     |  オン    |  **フォールバックなし**: 現在の境界グループ内の配布ポイントのみを使用します。       
オン     |  オフ|  **フォールバックなし**: 現在の境界グループ内の配布ポイントのみを使用します。       
オフ |  オフ|  **近隣ノードへのフォールバック**: 現在の境界グループ内の配布ポイントを使用し、近隣境界グループから配布ポイントを追加します。 既定のサイトの境界グループに明示的なリンクを構成しない限り、クライアントはそのグループにフォールバックしません。    
オフ | オン        |   **通常のフォールバック**: 現在の境界グループ内の配布ポイントを使用してから、近隣ノードとサイトの既定の境界グループから配布ポイントを使用します。

 その他のすべての展開の構成は**通常のフォールバック**になります。  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>コンテンツの場所の UI と動作に関する旧バージョンからの変更点
境界グループとクライアントのコンテンツ検索方法への主な変更を次に示します。 これらの変更はバージョン 1610 で導入されました。 これらの変更と概念の多くが連動しています。


-    **高速または低速の構成の削除:** 個々の配布ポイントに高速または低速を設定する必要がなくなりました。  代わりに、境界グループに関連付けられている各サイト システムが同じように処理されます。 この変更により、境界グループ プロパティの [**参照**] タブで高速または低速の構成がサポートされなくなりました。
-     **各サイトに新しい既定の境界グループ:** 各プライマリ サイトに ***Default-Site-Boundary-Group&lt;sitecode>*** という名前の新しい既定の境界グループが追加されました。  クライアントが境界グループに割り当てられているネットワークの場所にいない場合、そのクライアントは、割り当てられたサイトの既定のグループに関連付けられているサイト システムを使用します。 フォールバックするコンテンツの場所の概念に代わるものとして、この境界グループを使用することを計画してください。      
 -    [**代替のコンテンツ ソースの場所の使用を許可する**] の削除: フォールバックに使用する配布ポイントを明示的に構成する必要がなくなったため、これを設定するオプションが UI から削除されました。

    さらに、アプリケーションの展開の種類で [**代替のコンテンツ ソースの場所の使用をクライアントに許可する**] の設定をオンにした場合の結果が変更されています。 展開の種類でこの設定をオンにすると、クライアントがコンテンツ ソースの場所として既定のサイトの境界グループを使用できるようになりました。

 -    **境界グループのリレーションシップ:** 各境界グループを 1 つ以上の別の境界グループにリンクできます。 これらのリンクは、**[リレーションシップ]** という名前の新しい境界グループ プロパティ タブに構成されるリレーションシップを形成します。
     -    クライアントに直接関連付けられている各境界グループは、**現在の**境界グループと呼ばれます。  
    -     クライアントの*現在の*境界グループと別のグループとの関連付けによりクライアントが使用できる境界グループはすべて、**近隣**境界グループと呼ばれます。
    -  これは [**リレーションシップ**] タブにあり、ここで*近隣*境界グループとして使用できる境界グループを追加します。 また、クライアントが*現在の*グループで配布ポイントからコンテンツを検索するのに失敗したと判断して、これらの*近隣*境界グループからコンテンツの場所の検索を開始する時間を分単位で設定することもできます。

        境界グループの構成を追加または変更する場合に、構成している現在のグループから特定の境界グループへのフォールバックをブロックするオプションがあります。

    新しい構成を使用するには、ある境界グループから別の境界グループに明示的な関連付け (リンク) を定義し、関連付けられているグループ内のすべての配布ポイントを同じ時間 (分単位) で設定します。 設定する時間によって、クライアントが*現在の*境界グループからのコンテンツ ソースの検索に失敗した場合に、近隣境界グループからコンテンツ ソースの検索を開始できる時間が決まります。

    明示的に設定した境界グループに加え、各境界グループには既定のサイト境界グループへの暗黙的なリンクもあります。 このリンクは、既定のサイトの境界グループが近隣境界グループになり、クライアントにコンテンツ ソースの場所としてその境界グループと関連付けられた配布ポイントを使用できるようになってから 120 分後にアクティブになります。

    これは、以前はコンテンツのフォールバックと呼ばれていた動作に取って代わるものです。  この 120 分の既定の動作は、既定のサイトの境界グループを*現在の*グループに明示的に関連付け、特定の時間を分単位で設定するか、フォールバックを完全にブロックして使用できないようにすることで無効にすることができます。


-     **クライアントは各配布ポイントからのコンテンツ取得を最大 2 分間試みる:** クライアントは、コンテンツ ソースの場所を検索する際に、各配布ポイントへのアクセスを 2 分間試行してから別の配布ポイントを試します。 これは、クライアントが配布ポイントへの接続を最大 2 時間試行していた以前のバージョンからの変更点です。

    - クライアントが使用を試みる最初の配布ポイントは、クライアントの*現在の*境界グループ (複数可) 内の利用可能な配布ポイントのプールからランダムに選択されます。

    - 2 分後に、クライアントがコンテンツを見つけられない場合は、新しい配布ポイントに切り替えて、そのサーバーからコンテンツを取得しようとします。 このプロセスは、クライアントがコンテンツを見つけるか、そのプール内の最後のサーバーに到達するまで 2 分ごとに繰り返されます。

    - クライアントが*近隣*境界グループへのフォールバック期間に達するまでに、*現在の*プールから有効なコンテンツ ソースの場所を見つけられない場合、クライアントはその*近隣*グループからの配布ポイントを現在のリストの末尾に追加して、両方の境界グループからの配布ポイントを含む拡張されたソースの場所のグループを検索します。

        > [!TIP]  
        > 現在の境界グループから既定のサイトの境界グループに明示的なリンクを作成し、近隣境界グループへのリンクのフォールバック時間よりも短いフォールバック時間を定義すると、クライアントは、近隣グループを含める前の既定のサイトの境界グループからのソースの場所の検索を開始します。

    - クライアントがプール内の最後のサーバーからのコンテンツの取得に失敗した場合、もう一度プロセスを開始します。


## <a name="procedures-for-boundary-groups"></a>境界グループの手順
次の手順はバージョン 1610 以降に適用されます。 使用しているバージョンが 1610 より前の場合、「[Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606)」(System Center Configuration Manager バージョン 1511、1602、1606 の境界グループ) の手順を参照してください。


### <a name="to-create-a-boundary-group"></a>境界グループを作成するには  
1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] >  [**境界グループ**] をクリックします。  

2.  **[ホーム]** タブの **[作成]** グループで、 **[境界グループの作成]**をクリックします。  

3.  **[境界グループの作成]** ダイアログ ボックスで、 **[全般]** タブを選択し、この境界グループの **[名前]** を指定します。  

4.  [OK] をクリックして新しい境界グループを保存します。 ****  


### <a name="to-configure-a-boundary-group"></a>境界グループを構成するには  
 1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] >  [**境界グループ**] をクリックします。  

 2.  変更する境界グループを選択します。  

 3.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

 4.  境界グループの **[プロパティ]** ダイアログ ボックスで、 **[全般]** タブを選択してこの境界グループのメンバーである境界を変更します。  

     -   境界を追加するには、 **[追加]**をクリックし、1 つまたは複数の境界のチェック ボックスを選択して、 **[OK]**をクリックします。  

     -   境界を削除するには、境界を選択して [削除] をクリックします。 ****  

 5.  **[参照]** タブを選択し、サイトの割り当てと、関連付けられたサイト システム サーバーの構成を変更します。  

     -   この境界グループをサイト割り当て用にクライアントが使用できるようにするには、 **[サイト割り当てにこの境界を使用する]**のチェック ボックスをオンにして、 **[割り当てられたサイト]** のドロップダウン ボックスからサイトを選択します。  

     -   この境界グループに関連付けられている使用可能なサイト システム サーバーを構成するには:  

     1.  [追加] をクリックし、1 つまたは複数のサーバーのチェック ボックスをオンにします。 **** サーバーは、この境界グループの関連付けられたサイト システム サーバーとして追加されます。 サーバーにインストールされたサイト システムの役割をサポートしているサーバーのみを利用できます。  

         > [!NOTE]  
         >  階層内のすべてのサイトから、利用可能なサイト システムの任意の組み合わせを選択できます。 選択したサイト システムは [サイト システム **** ] タブで、この境界グループのメンバーの各境界のプロパティに一覧表示されます。  

     2.  サーバーを境界グループから削除するには、サーバーを選択して **[削除]**をクリックします。  

         > [!NOTE]  
         >  この境界グループが関連するサイト システムに使用されないようにするには、関連付けられたサイト システム サーバーとして表示されているすべてのサーバーを削除する必要があります。  

 6.  **[関係]** タブを選択して、フォールバック動作を構成します。  

     - **[追加]** をクリックし、構成する境界グループを選択します。

     - 配布ポイントのフォールバック時間を設定します。 この時間が経過すると、関係を構成する境界グループのクライアントは、追加する境界グループの配布ポイントからコンテンツを検索できるようになります。

     - 既定で構成されている*既定のサイト境界グループ*を含め、特定の境界グループへのフォールバックを回避するには、境界グループを選択し、**[Never fallback]** (フォールバックしない) をオンにします。   

 7.  [OK] をクリックして境界グループのプロパティを閉じ、構成を保存します。 ****  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>サイト システム サーバーを境界グループに関連付けるには  
 1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] >  [**境界グループ**] をクリックします。  

 2.  変更する境界グループを選択します。  

 3.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

 4.  境界グループの **[プロパティ]** ダイアログ ボックスで、 **[参照]** タブを選択します。  

 5.  **[サイト システム サーバーの選択]**にある **[追加]**をクリックし、この境界グループに関連付けるサイト システム サーバーのチェック ボックスをオンにして **[OK]**をクリックします。  

 6.  [OK] をクリックしてダイアログ ボックスを閉じ、境界グループの構成を保存します。 ****  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>サイトの自動割り当てのフォールバック サイトを構成するには  

  1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] >  [**サイト**] の順にクリックします。  

  2.  **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]**をクリックします。  

  3.  **[全般]** タブで、 **[フォールバック サイトを使用する]**のチェック ボックスをオンにして、 **[フォールバック サイト]** のドロップダウン リストからサイトを選択します。  

  4.  [ **OK** ] をクリックして構成を保存します。  

#### <a name="to-enable-use-of-preferred-management-points"></a>優先管理ポイントの使用を有効にする  

 1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] > [**サイト**] の順にクリックし、[**ホーム**] タブの [**階層設定**] をクリックします。  

 2.  [階層設定] の **[全般]** タブで、 **[クライアントは境界グループで指定された管理ポイントの使用を優先]**を選択します。  

 3.  **[OK]** をクリックしてダイアログ ボックスを閉じ、構成を保存します。  

