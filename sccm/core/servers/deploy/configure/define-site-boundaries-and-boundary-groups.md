---
title: "サイト境界の定義 | System Center Configuration Manager"
description: "管理するデバイスを含めることができる、イントラネット上のネットワークの場所を定義する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト境界と境界グループの定義

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の境界は、管理するデバイスを含めることができる、イントラネット上のネットワークの場所を定義します。 境界グループは、構成する対象となる境界の論理的なグループです。 境界グループと境界は、どちらも階層全体で使用可能で、個々のサイトに対して構成する必要はありません。  

 階層には、任意の数の境界グループを含めることができ、各境界グループには、次の境界の種類のあらゆる組み合わせを含めることができます。  

-   IP サブネット、  

-   Active Directory サイト名  

-   IPv6 プレフィックス  

-   IP アドレスの範囲  

イントラネット上のクライアントは、現在のネットワークの場所を評価し、所属する境界グループを識別するためにその情報を使用します。  

 クライアントは、次の目的で境界グループを使用します。  

-   **割り当て済みサイトの検索:** 境界グループを使用することで、クライアントによるクライアント割り当て用のプライマリ サイトの検出を有効にします (サイトの自動割り当て)。  

-   **使用できる特定のサイト システムの役割の検索:**  境界グループを特定のサイト システムの役割と関連付けると、境界グループによって、クライアントにサイト システムの一覧が提供され、コンテンツの検索時に使用したり、優先する管理ポイントとして使用したりすることができます。  

インターネット上のクライアントまたはインターネット専用として構成されたクライアントは、境界情報を使用しません。 これらのクライアントはサイトの自動割り当てを使用できないため、インターネットを介したクライアント接続を許可するように配布ポイントが構成されている場合は、いつでも割り当て済みサイトの配布ポイントからコンテンツをダウンロードできます。  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> 境界  
 個別の境界を手動で作成できます。 さらに、[Active Directory フォレスト探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) を構成すると、自動検出を実行し、検出された各 IP サブネットと Active Directory サイトに対して境界を作成します。  

-   各境界はネットワークの場所を示し、階層内の全サイトから利用できます。  

-   Configuration Manager では、境界としてスーパーネットを直接入力できません。 代わりに、境界の種類として IP アドレスの範囲を使用してください。  

-   Active Directory フォレストの探索によって、Active Directory サイトに割り当てられているスーパーネットが特定されると、Configuration Manager はスーパーネットを IP アドレスの範囲の境界に変換します。  

-   クライアントが存在する境界は、Active Directory サイトに相当します。つまり、クライアントが識別するネットワーク IP アドレスに相当します。 (クライアントが、Configuration Manager 管理者によって認識されない IP アドレスを使用することは珍しくありません。 ネットワークの上でのクライアントの場所に疑問がある場合は、クライアント上で **IPCONFIG** コマンドを使用して、クライアントがレポートする場所を確認します。)  

境界を作成すると、境界の種類とスコープに基づいて自動的に名前が付けられます。 この名前は変更できません。 ただし、Configuration Manager コンソールで境界を識別しやすいように、境界の構成時に説明を入力できます。  

 境界を作成した後でプロパティを変更して、次の操作を行うことができます。  

-   1 つまたは複数の境界グループに境界を追加する。  

-   境界の種類またはスコープを変更する。  

-   境界の **[サイト システム]** タブで、境界に関連付けられたサイト システム サーバー (配布ポイント、状態移行ポイント、および管理ポイント) を確認します。  

#### <a name="to-create-a-boundary"></a>境界を作成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] > [**境界**] をクリックします。  

2.   **[ホーム]** タブの **[作成]** グループで、 **[作成] Boundary.**をクリックします。  

3.  [境界の作成] ダイアログ ボックスの **[全般]** タブで、 **[説明]** を指定して、フレンドリ名または参照によって境界を識別します。  

4.  この境界の [種類] を選択します。 ****  

    -   **[IP サブネット]**を選択した場合、この境界の **サブネット ID** を指定する必要があります。  

        > [!TIP]  
        >  **[ネットワーク]** と **[サブネット マスク]** を指定すると、 **サブネット ID** を自動的に取得できます。 境界を保存すると、サブネット ID 値だけが保存されます。  

    -   **[Active Directory サイト]**を選択した場合、サイト サーバーのローカル フォレスト内の Active Directory サイトを指定するか、その場所を **[参照]** する必要があります。  

        > [!IMPORTANT]  
        >  境界の Active Directory サイトを指定すると、Active Directory サイトのメンバーである各 IP サブネットが境界に含まれます。 Active Directory で Active Directory サイトの構成が変更されると、この境界に含まれているネットワークの場所も変更されます。  

    -   **[IPv6 プレフィックス]**を選択した場合、IPv6 プレフィックス形式で **[プレフィックス]** を指定する必要があります。  

    -   **[IP アドレスの範囲]**を選択した場合、IP サブネットの一部または複数の IP サブネットを含む **[開始 IP アドレス]** と **[終了 IP アドレス]** を指定する必要があります。  

5.  [OK] をクリックして新しい境界を保存します。 ****  

#### <a name="to-configure-a-boundary"></a>境界を構成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] > [**境界**] をクリックします。  

2.  変更する境界を選択します。  

3.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

4.  境界の **[プロパティ]** ダイアログ ボックスで、 **[全般]** タブを選択して、境界の **[説明]** または **[種類]** を編集します。 境界のネットワークの場所を編集して、境界のスコープを変更することもできます。 たとえば、Active Directory サイトの境界の場合、新しい Active Directory サイト名を指定できます。  

5.  [サイト システム **** ] タブを選択し、その境界に関連付けられているサイト システムを確認します。 この構成は、境界のプロパティから変更することはできません。  

    > [!TIP]  
    >  サイト システム サーバーが境界のサイト システムの一覧に表示されるようにするには、サイト システム サーバーが、この境界を含む、少なくとも 1 つの境界グループのサイト システム サーバーとして関連付けられている必要があります。 これは、境界グループの **[参照]** タブで構成されます。  

6.  [境界グループ] タブを選択して、この境界の境界グループ メンバーシップを変更します。 ****  

    -   この境界を 1 つまたは複数の境界グループに追加するには、 **[追加]**をクリックして、1 つまたは複数の境界グループのチェック ボックスをオンにし、 **[OK]**をクリックします。  

    -   この境界を境界グループから削除するには、境界グループを選択して [削除] をクリックします。 ****  

7.  [OK] をクリックして境界のプロパティを閉じ、構成を保存します。 ****  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 境界グループを作成すると、関連するネットワークの場所 (境界) を論理的にグループ化して、インフラストラクチャを管理しやすくできます。 境界グループを使用するには、先に境界を境界グループに割り当てておく必要があります。 クライアントは、次の目的で境界グループの構成を使用します。  

-   サイトの自動割り当て  

-   コンテンツの場所  

-   優先管理ポイント (優先管理ポイントを使用する場合は、境界グループの構成内ではなく、階層に対してこのオプションを有効にする必要があります。 次の手順の「 *優先管理ポイントの使用を有効にする*」を参照してください。)  

境界グループの構成時には、境界グループに 1 つまたは複数の境界を追加し、これらの境界に配置されているクライアント用の追加の設定を構成します。  

#### <a name="to-create-a-boundary-group"></a>境界グループを作成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] >  [**境界グループ**] をクリックします。  

2.  **[ホーム]** タブの **[作成]** グループで、 **[境界グループの作成]**をクリックします。  

3.  **[境界グループの作成]** ダイアログ ボックスで、 **[全般]** タブを選択し、この境界グループの **[名前]** を指定します。  

4.  [OK] をクリックして新しい境界グループを保存します。 ****  

#### <a name="to-configure-a-boundary-group"></a>境界グループを構成するには  

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

    3.  この境界グループのサイト システム サーバーのネットワーク接続速度を変更するには、サーバーを選択して **[接続の変更]**をクリックします。  

         既定では、各サイト システムの接続速度は **[高速]**になっていますが、 **[低速]**に変更できます。 ネットワーク接続速度と展開の構成を基に、クライアントがコンテンツをサーバーからダウンロードできるかどうかが決定されます。  

6.  [OK] をクリックして境界グループのプロパティを閉じ、構成を保存します。 ****  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>コンテンツ展開サーバーまたは管理ポイントを境界グループに関連付けるには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] >  [**境界グループ**] をクリックします。  

2.  変更する境界グループを選択します。  

3.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

4.  境界グループの **[プロパティ]** ダイアログ ボックスで、 **[参照]** タブを選択します。  

5.  **[サイト システム サーバーの選択]**にある **[追加]**をクリックし、この境界グループに関連付けるサイト システム サーバーのチェック ボックスをオンにして **[OK]**をクリックします。  

6.  [OK] をクリックしてダイアログ ボックスを閉じ、境界グループの構成を保存します。 ****  

#### <a name="to-enable-use-of-preferred-management-points"></a>優先管理ポイントの使用を有効にする  

1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] > [**サイト**] の順にクリックし、[**ホーム**] タブの [**階層設定**] をクリックします。  

2.  [階層設定] の **[全般]** タブで、 **[クライアントは境界グループで指定された管理ポイントの使用を優先]**を選択します。  

3.  **[OK]** をクリックしてダイアログ ボックスを閉じ、構成を保存します。  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>サイトの自動割り当てのフォールバック サイトを構成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] >  [**サイト**] の順にクリックします。  

2.  **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]**をクリックします。  

3.  **[全般]** タブで、 **[フォールバック サイトを使用する]**のチェック ボックスをオンにして、 **[フォールバック サイト]** のドロップダウン リストからサイトを選択します。  

4.  [ **OK** ] をクリックして構成を保存します。  

 次のセクションでは、境界グループの構成に関する追加情報について説明します。  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> サイトの割り当てについて  
 各境界グループごとに、クライアント用の割り当てられたサイトを構成できます。  

-   サイトの自動割り当てを使用する新しくインストールされたクライアントは、クライアントの現在のネットワークの場所を含む境界グループの割り当て済みサイトに参加します。  

-   サイトに割り当てられると、クライアントがネットワークの場所を変更するときに、クライアントのサイトの割り当てが変更されることはありません。 たとえば、別のサイトが割り当てられた境界グループ内の境界が示されている新しいネットワークの場所にクライアントがローミングしたとしても、クライアントに対して割り当てられたサイトが変更されることはありません。  

-   Active Directory システムの探索で新しいリソースが検出されると、検出されたリソースのネットワーク情報が境界グループ内の境界に対して評価されます。 このプロセスにより、割り当てられたサイトに新しいリソースが関連付けられ、クライアント プッシュ インストール方法で使用できるようになります。  

-   境界が、異なる割り当て済みサイトを持つ複数の境界グループのメンバーである場合は、クライアントによってランダムにいずれかのサイトが選択されます。  

-   境界グループの割り当て済みサイトへの変更は、新しいサイトの割り当て操作にのみ適用されます。 以前にサイトに割り当て済みのクライアントは、境界グループの構成の変更 (またはクライアントのネットワークの場所の変更) に基づくサイトの割り当てを再評価しません。  

クライアントのサイトの割り当ての詳細については、「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../../core/clients/deploy/assign-clients-to-a-site.md)」の「[コンピューターにサイトの自動割り当てを使用する](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment)」をご覧ください。  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> コンテンツの場所について  
 各境界グループに 1 つまたは複数の配布ポイントと状態移行ポイントを含めるよう構成し、同じ配布ポイントと状態移行ポイントを複数の境界グループに関連付けることができます。  

-   **ソフトウェアの配布時に**、クライアントは展開コンテンツ用の場所を要求します。 Configuration Manager は、クライアントの現在のネットワークの場所を含む各境界グループに関連付けられた配布ポイントのリストをクライアントに送信します。  

-   **オペレーティング システムの展開時に、クライアントは** 状態移行情報の送受信用の場所を要求します。 Configuration Manager は、クライアントの現在のネットワークの場所を含む、各境界グループに関連付けられた状態移行ポイントのリストをクライアントに送信します。  

この動作により、コンテンツまたは状態移行情報の転送元となる最も近いサーバーをクライアントが選択できるようになります。  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> 優先管理ポイントについて  
 優先管理ポイントを使用すると、クライアントは、その現在のネットワークの場所 (境界) に関連付けられた管理ポイントを特定できます。  

-   クライアントは、優先として構成されていない割り当て済みサイトからの管理ポイントを使用する前に、割り当て済みサイトからの優先管理ポイントを使用しようとします。  

-   このオプションを使用するには、それを階層に対して有効にして、境界グループの関連境界に関連付ける必要がある管理ポイントを含めるように個々のプライマリ サイトの境界グループを構成する必要があります。  

-   優先管理ポイントが構成され、クライアントが管理ポイントの一覧を整理するときに、割り当て済み管理ポイントの一覧 (クライアントの割り当て済みサイトからのすべての管理ポイントを含む) の一番上に優先管理ポイントがクライアントにより配置されます。  

> [!NOTE]  
>  クライアントのローミング時 (ラップトップ コンピューターをリモート オフィスに持って行くときなど、クライアントのネットワークの場所を変更するとき) に、クライアントは新しい場所でローカル サイトからの管理ポイント (またはプロキシ管理ポイント) を使用してから、割り当て済みサイト (優先管理ポイントがあるサイト) からの管理ポイントを使用する場合があります。  詳細については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」をご覧ください。  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> 重複する境界について  
 Configuration Manager は、コンテンツの場所について、重複する境界を持つ構成をサポートします。  

-   **クライアントがコンテンツを要求し**、クライアントのネットワークの場所が複数の境界グループに属している場合、Configuration Manager はコンテンツが格納されているすべての配布ポイントのリストをクライアントに送信します。  

-   **クライアントが状態移行情報の送受信をサーバーに要求し**、クライアントのネットワークの場所が複数の境界グループに属している場合は、Configuration Manager は、クライアントの現在のネットワークの場所を含む境界グループに関連付けられた状態移行ポイントのリストをクライアントに送信します。  

この動作により、コンテンツまたは状態移行情報の転送元となる最も近いサーバーをクライアントが選択できるようになります。  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> ネットワーク接続速度について  
 境界グループ内の各サイト システム サーバーのネットワーク接続速度を設定できます。 この設定は、この境界グループの構成に基づいてサイト システムに接続するクライアントに適用されます。 異なる境界グループ内で、同じサイト システム サーバーに異なる接続速度を設定できます。  

 ネットワーク接続速度は既定で [ **高速**] に構成されていますが、[ **低速**] に構成することもできます。 ネットワーク接続速度と展開構成を基に、クライアントが関連付けられた境界グループ内にある場合に、コンテンツを配布ポイントからダウンロードできるかどうかが決定されます。  

 ネットワーク接続速度の構成がクライアントのコンテンツ取得方法に及ぼす影響の詳細については、「[コンテンツ ソースの場所の例](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md)」をご覧ください。  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> 境界について推奨する運用方法  

-   **IP アドレスの範囲の境界の種類は、他の境界の種類を使用できない場合にのみ、使用することを検討してください。**  

     境界の戦略を策定するときは、その他の境界の種類を使用する前に、Active Directory サイトに基づく境界を使用することを推奨します。 Active Directory サイトに基づく境界を使用できない場所では、IP サブネットまたは IPv6 境界を使用します。 これらのオプションのいずれも使用できない場合、IP アドレス範囲の境界を使用します。 これは、サイトでは境界のメンバーを定期的に評価し、IP アドレス範囲のメンバーの評価に必要なクエリでは、その他の境界の種類のメンバーを評価するクエリよりも、かなり多くの SQL Server リソースが必要なためです。  

-   **サイトの自動割り当てでは、重複する境界を避けてください。**  

     各境界グループは、サイト割り当ての構成とコンテンツの場所の構成をサポートしていますが、運用方法としては、サイトの割り当てのみに使用する境界グループのセットを個別に作成することをお勧めします。 意味: 境界グループ内の各境界が、異なるサイトの割り当てが指定された別の境界グループのメンバーになっていないことを確認してください。 その理由:  

    -   1 つの境界を、複数の境界グループに含めることができます。  

    -   各境界グループは、サイト割り当てのための別のプライマリ サイトを関連付けることができます。  

    -   異なるサイトの割り当てが指定された 2 つの別の境界グループのメンバーである境界にクライアントが配置されていると、そのクライアントは参加するサイトをランダムに選択します。ただし、そのサイトはクライアントが参加する予定のサイトではない可能性があります。  この構成は、重複する境界と呼ばれます。  

     重複する境界は、コンテンツの場所に関しては問題とはなりません。むしろ、多くの場合、使用できる他のリソースやコンテンツの場所をクライアントに提供するのに適した構成となります。  



<!--HONumber=Nov16_HO1-->

