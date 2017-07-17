---

title: "ソフトウェア更新プログラムの手動展開 | Microsoft ドキュメント"
description: "更新プログラムを手動で展開するには、Configuration Manager コンソールで更新プログラムを選んで手動で展開するか、または更新プログラムを更新プログラム グループに追加してグループを展開します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.translationtype: Human Translation
ms.sourcegitcommit: c6ee0ed635ab81b5e454e3cd85637ff3e20dbb34
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.contentlocale: ja-jp
ms.lasthandoff: 06/08/2017


---

#  <a name="BKMK_ManualDeploy"></a> ソフトウェア更新プログラムの手動展開  

*適用対象: System Center Configuration Manager (Current Branch)*

 ソフトウェア更新プログラムの手動展開は、Configuration Manager コンソールでソフトウェア更新プログラムを選び、展開プロセスを手動で開始するプロセスです。 または、選択したソフトウェア更新プログラムを更新プログラム グループに追加して、手動で更新プログラム グループを展開できます。 通常は、手動展開によって、必要なソフトウェア更新プログラムを適用してクライアント デバイスを最新の状態にした後で、月 1 回の継続的なソフトウェア更新プログラムの展開を管理する ADR を作成します。 また、帯域外のソフトウェア更新プログラムの展開にも手動展開を使用します。 どちらの展開方法が適しているか判断する場合は、「[ソフトウェアの更新を展開する](deploy-software-updates.md)」を参照してください。

 以下のセクションでは、ソフトウェア更新プログラムを手動で展開する手順について説明します。  

##  <a name="BKMK_1SearchCriteria"></a> 手順 1: ソフトウェア更新プログラムの検索条件を指定する  
 Configuration Manager コンソールに表示されるソフトウェア更新プログラムの数は、数千個になることがあります。 手動でのソフトウェア更新プログラムの展開のワークフローでは、第一段階として、展開するソフトウェア更新プログラムを特定します。 たとえば、50 を超えるクライアント デバイスで必要であり、「 **セキュリティ** 」または「 **重大** 」に分類されているすべてのソフトウェア更新プログラムを取得するというような条件を指定できます。  

> [!IMPORTANT]  
>  1 回のソフトウェア更新プログラムの展開に含めることができるソフトウェア更新プログラムの最大数は、1000 です。  

#### ソフトウェア更新プログラムの検索条件を指定するには
<a id="to-specify-search-criteria-for-software-updates" class="xliff"></a>  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ] ワークスペースで [ソフトウェア更新プログラム ****] を展開して、[すべてのソフトウェア更新プログラム ****] をクリックします。 同期済みのソフトウェア更新プログラムが表示されます。  

    > [!NOTE]  
    >  Configuration Manager の **[すべてのソフトウェア更新プログラム]** ノードには、**[重大]** および **[セキュリティ]** に分類され、過去 30 日以内にリリースされたソフトウェア更新プログラムのみが表示されます。  

3.  検索パネルで、次の手順のいずれか、または両方を使用して、必要なソフトウェア更新プログラムを絞り込みます。  

    -   検索テキスト ボックスに、ソフトウェア更新プログラムを絞り込む検索文字列を入力します。 たとえば、特定のソフトウェア更新プログラムのアーティクル ID やセキュリティ情報 ID を入力するか、複数のソフトウェア更新プログラムのタイトルに使用されている可能性のある文字列を入力します。  

    -   [条件の追加 ****] をクリックしてソフトウェア更新プログラムの絞り込みに使用する条件を選択し、[追加 ****] をクリックして条件の値を指定します。  

4.  [検索 **** ] をクリックして、ソフトウェア更新プログラムを絞り込みます。  

    > [!TIP]  
    >  [検索 **** ] タブおよび [保存 **** ] グループに、フィルター条件を保存するためのオプションがあります。  

##  <a name="BKMK_2UpdateGroup"></a> 手順 2: ソフトウェア更新プログラムを含むソフトウェア更新プログラム グループを作成する  
 ソフトウェア更新プログラム グループは、展開に備えてソフトウェア更新プログラムを整理するための有効な手段です。 ソフトウェア更新プログラムをソフトウェア更新プログラム グループに手動で追加したり、Configuration Manager の ADR を使用して、新規または既存のソフトウェア更新プログラム グループに自動的に追加したりできます。 ソフトウェア更新プログラムを新しいソフトウェア更新プログラム グループに手動で追加するには、次の手順に従います。  

#### ソフトウェア更新プログラムを新しいソフトウェア更新プログラム グループに手動で追加するには
<a id="to-manually-add-software-updates-to-a-new-software-update-group" class="xliff"></a>  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ] ワークスペースで、[ソフトウェア更新プログラム ****] をクリックします。  

3.  新しいソフトウェア更新プログラム グループに追加するソフトウェア更新プログラムを選択します。  

4.  [ホーム **** ] タブの [更新 **** ] グループで、[ソフトウェア更新プログラム グループの作成 ****] をクリックします。  

5.  ソフトウェア更新プログラム グループの名前を指定し、必要に応じて説明を入力します。 名前と説明によって、ソフトウェア更新プログラム グループに含まれているソフトウェア更新プログラムの種類を判別できる情報を指定します。 [作成 ****] をクリックします。  

6.  [ソフトウェア更新プログラム グループ **** ] ノードをクリックして、新しいソフトウェア更新プログラム グループを表示します。  

7.  ソフトウェア更新プログラム グループを選択し、[ホーム **** ] タブの [更新 **** ] グループで [メンバーの表示 **** ] をクリックして、グループに含まれているソフトウェア更新プログラムの一覧を表示します。  

##  <a name="BKMK_3DownloadContent"></a> 手順 3: ソフトウェア更新プログラム グループのコンテンツをダウンロードする  
 必要に応じて、ソフトウェア更新プログラムを展開する前に、ソフトウェア更新プログラム グループに含めるソフトウェア更新プログラムのコンテンツをダウンロードできます。 この方法を選択すると、ソフトウェア更新プログラムを展開する前に、そのコンテンツが配布ポイントで使用可能になっていることを確認できます。 これにより、コンテンツの配布に関して、予期せぬ問題を回避できます。 この手順は省略することができ、その場合、コンテンツは展開プロセスの過程で配布ポイントにダウンロードされ、コピーされます。 ソフトウェア更新プログラムのコンテンツをソフトウェア更新プログラム グループにダウンロードするには、次の手順に従います。  



#### ソフトウェア更新プログラム グループにコンテンツをダウンロードするには
<a id="to-download-content-for-the-software-update-group" class="xliff"></a>
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### コンテンツのステータスを監視するには
<a id="to-monitor-content-status" class="xliff"></a>
1. ソフトウェア更新プログラムのコンテンツのステータスを監視するには、Configuration Manager コンソールで **[監視]** をクリックします。  

2. [監視] ワークスペースで、[配布ステータス ****] を展開して、[コンテンツのステータス ****] をクリックします。  

3. ソフトウェア更新プログラム グループにソフトウェア更新プログラムをダウンロードするために、事前に特定したソフトウェア更新パッケージを選択します。  

4. [ホーム **** ] タブの [コンテンツ **** ] グループで、[ステータスの表示 ****] をクリックします。  

##  <a name="BKMK_4DeployUpdateGroup"></a> 手順 4: ソフトウェア更新プログラム グループを展開する  
 展開するソフトウェア更新プログラムを判別してソフトウェア更新プログラム グループに追加したら、ソフトウェア更新プログラム グループ内のソフトウェア更新プログラムを手動で展開できます。 ソフトウェア更新プログラム グループ内のソフトウェア更新プログラムを手動で展開するには、次の手順に従います。  

#### ソフトウェア更新プログラム グループ内のソフトウェア更新プログラムを手動で展開するには
<a id="to-manually-deploy-the-software-updates-in-a-software-update-group" class="xliff"></a>  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ] ワークスペースで [ソフトウェア更新プログラム ****] を展開して、[ソフトウェア更新プログラム グループ ****] をクリックします。  

3.  展開するソフトウェア更新プログラム グループを選択します。  

4.  [ **ホーム** ] タブの [ **展開** ] グループで、[ **展開**] をクリックします。 **ソフトウェア更新プログラムの展開ウィザード** が開きます。  

5.  [全般] ページで、次の設定を構成します。  

    -   **名前**: 展開の名前を指定します。 展開の名前は、一意であり、展開の目的を示し、Configuration Manager サイト内の他の展開と区別できるものでなければなりません。 既定では、Configuration Manager により、自動的に展開の名前が次の形式で指定されます。**Microsoft Software Updates -** <*日付*><*時刻*>  

    -   **説明**: 展開の説明を指定します。 説明では、展開の概要、および、Configuration Manager サイト内の他の展開と区別するのに役立つその他の関連情報を示します。 説明フィールドは省略可能で、256 文字以内で指定する必要があります。既定値は空白です。  

    -   **ソフトウェア更新プログラム/ソフトウェア更新プログラム グループ**: 表示されたソフトウェア更新プログラム グループ、または、ソフトウェア更新プログラムが正しいことを確認します。  

    -   **展開テンプレートの選択**: 既に保存されている展開テンプレートを適用するかどうかを指定します。 複数の一般的なソフトウェア更新プログラムの展開プロパティを含む展開テンプレートを構成して、以降、ソフトウェア更新プログラムを展開する際に適用し、同じような展開で整合性を確保したり、時間を節約したりできます。  

    -   **コレクション**: 適切に展開のコレクションを指定します。 コレクションのメンバーは、展開で定義されたソフトウェア更新プログラムを受信します。  

6.  [展開設定] ページで、次の設定を構成します。  

    -   **展開の種類**: ソフトウェア更新プログラムの展開の種類を指定します。 構成されたインストール期限までにソフトウェア更新プログラムがクライアントで自動的にインストールされる必須のソフトウェア更新プログラムの展開を作成するには、[ **必須** ] を選択します。 ユーザーがソフトウェア センターから入手できるオプションのソフトウェア更新プログラムの展開を作成するには、[ **利用可能** ] を選択します。  

        > [!IMPORTANT]  
        >  ソフトウェア更新プログラムの展開を作成した後に展開の種類を変更することはできません。  

        > [!NOTE]  
        >  **[必須]** として展開されているソフトウェア更新プログラム グループは、バック グラウンドでダウンロードされ、BITS 設定に従います (構成されている場合)。  
        > ただし、 **[利用可能]** として展開されているソフトウェア更新プログラム グループは、フォア グラウンドでダウンロードされ、BITS 設定を無視します。  

    -   **展開が必要なときに、Wake-on-LAN を使用してクライアントを起動する**: 期限になったら Wake On LAN を有効にして、展開の 1 つまたは複数のソフトウェア更新プログラムを必要とするコンピューターにウェイクアップ パケットを送信するかどうかを指定します。 スリープ モードのコンピューターは、ソフトウェア更新プログラムのインストールを開始できるように、インストール期限になるとスリープ解除されます。 展開のソフトウェア更新プログラムを必要としないクライアントは起動されません。 既定では、この設定は無効になっており、[ **展開の種類** ] が [ **必須** ] に設定されている場合にのみ使用することができます。  

        > [!WARNING]  
        >  このオプションを使用する前に、コンピューターおよびネットワークを Wake On Lan 用に構成する必要があります。  

    -   **詳細レベル**: クライアント コンピューターによって報告される状態メッセージの詳細レベルを指定します。  

7.  [スケジュール] ページで、次の設定を構成します。  

    -   **スケジュールの評価**: 使用可能な時間およびインストール期限の時間を UTC と Configuration Manager コンソールを実行するコンピューターのローカル時刻のどちらを使用して評価するかを指定します。  

        > [!NOTE]  
        >  ローカル時刻を選択し、**[ソフトウェアが使用可能な時間]** または **[インストールの期限]** で **[直ちに]** を選択した場合は、Configuration Manager コンソールを実行しているコンピューターの現在の時刻を使用して、更新プログラムを利用可能にする時間またはクライアントにインストールする時間が評価されます。 クライアントのタイム ゾーンが異なる場合は、クライアントの時刻が評価時刻になったときにこれらのアクションが実行されます。  

    -   **ソフトウェアが使用可能な時間**: 次の設定のいずれかを選んで、クライアントでソフトウェア更新プログラムを利用可能にする時間を指定します。  

        -   **直ちに**: 展開のソフトウェア更新プログラムを直ちにクライアントで実行可能にします。 展開が作成されると、クライアント ポリシーが更新され、クライアントが次回のクライアント ポリシー ポーリング サイクルで展開を認識し、ソフトウェア更新プログラムがインストール可能になります。  

        -   **指定した時間経過後**: 展開のソフトウェア更新プログラムを特定の日時にクライアントで実行可能にします。 展開が作成されると、クライアント ポリシーが更新され、クライアントが次回のクライアント ポリシー ポーリング サイクルで展開を認識します。 ただし、展開のソフトウェア更新プログラムは、指定した日付と時刻になるまで、インストールに使用できません。  

    -   **インストールの期限**: 次の設定のいずれかを選んで、展開のソフトウェア更新プログラムのインストール期限を指定します。  

        > [!NOTE]  
        >  インストール期限の設定を構成できるのは、[展開設定] ページで [展開の種類 **** ] が [必須 **** ] に設定されている場合のみです。  

        -   **直ちに**: 展開のソフトウェア更新プログラムを直ちに自動インストールします。  

        -   **指定した時間経過後**: 展開のソフトウェア更新プログラムを特定の日時に自動インストールします。  

        > [!NOTE]  
        >  実際のインストール期限は、構成された特定の時刻に 2 時間までの任意の時間が加えられた時刻になります。 そのようにすることで、ターゲット コレクションのすべてのクライアント コンピューターで、同時に展開のソフトウェア更新プログラムがインストールされないようにしています。  
        >   
        >  **[コンピューター エージェント]** クライアント設定で **[期限のランダム化を無効にする]** を構成して、必要なソフトウェア更新プログラムのインストールの遅延のランダム化を無効にできるようになっています。 詳細については、「 [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent)」をご覧ください。  

8.  [ユーザー側の表示と操作] ページで、次の設定を構成します。  

    -   **ユーザーへの通知**: 構成された **[ソフトウェアが使用可能な時間]** に、クライアント コンピューターでソフトウェア センターにソフトウェア更新プログラムの通知を表示するかどうか、またユーザーへの通知をクライアント コンピューターで表示するかどうかを指定します。 [展開設定] ページで [展開の種類 **** ] が [利用可能 **** ] に設定されている場合、[すべての通知をソフトウェア センターで非表示にし、ユーザーにも通知しない ****] を選択することはできません。  

    -   **期限に達したときの操作**: *[展開設定] ページで* ***[展開の種類]** が **[必須]** に設定されている場合にのみ使用できます*。   
    ソフトウェア更新プログラムの展開の期限に達したときに実行する操作を指定します。 展開のソフトウェア更新プログラムをインストールするかどうかを指定します。 また、構成されたメンテナンス期間に関係なく、ソフトウェア更新プログラムのインストール後に、システムの再起動を実行するかどうかを指定します。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。  

    -   **デバイスの再起動**: *[展開設定] ページで* ***[展開の種類]** が **[必須]** に設定されている場合にのみ使用できます*。    
    ソフトウェア更新プログラムをインストールした後にサーバーおよびワークステーションでシステムの再起動を抑制するかどうか、また、インストールを完了するためにシステムの再起動が必要かどうかを指定します。  

        > [!IMPORTANT]  
        >  システムの再起動を抑制することは、サーバー環境や、ソフトウェア更新プログラムをインストールするコンピューターを、既定では再起動しない場合に役立ちます。 ただし、この場合、コンピューターが安全ではない状態のままになることがあります。一方、強制的に再起動すると、ソフトウェア更新プログラムのインストールをすぐに完了できます。

    -   **Windows Embedded デバイスに対してフィルター処理を書き込む**: 書き込みフィルターが有効にされた Windows Embedded デバイスにソフトウェア更新プログラムを展開するときに、ソフトウェア更新プログラムを一時オーバーレイにインストールし、変更を後でコミットするか、インストール期限またはメンテナンス期間中に変更をコミットするかを指定できます。 インストールの期限またはメンテナンス期間中に変更をコミットする場合は、再起動が必要になります。再起動すると、デバイスに変更が保持されます。  

        > [!NOTE]  
        >  ソフトウェア更新プログラムを Windows Embedded デバイスに展開する場合、デバイスが、メンテナンス期間が構成されたコレクションのメンバーであることを確認します。  

    - **再起動後のソフトウェア更新プログラムの展開の再評価動作**: Configuration Manager バージョン 1606 で開始した場合は、この設定を選択してソフトウェア更新プログラムの展開を構成します。これにより、クライアントはソフトウェア更新プログラムをインストールして再起動した後すぐに、ソフトウェア更新プログラムのコンプライアンス対応スキャンを実行するようになります。 これにより、クライアントは、クライアントの再起動後に適用可能になる追加のソフトウェア更新プログラムをチェックして、同じメンテナンス期間中にそれらをインストール (およびコンプライアンスに準拠) できます。

9. [アラート] ページで、Configuration Manager および System Center Operations Manager がこの展開のアラートを生成する方法を構成します。 アラートを構成できるのは、[展開設定] ページで [展開の種類 **** ] が [必須 **** ] に設定されている場合のみです。  

    > [!NOTE]  
    >  ソフトウェア更新プログラムに関する最新のアラートは、[ソフトウェア ライブラリ **** ] ワークスペースの [ソフトウェア更新プログラム **** ] ノードで確認することができます。  

10. [ダウンロードの設定] ページで、次の設定を構成します。  

    - クライアントが低速ネットワークに接続している場合、または、代替のコンテンツの場所を使用している場合に、クライアントでソフトウェア更新プログラムをダウンロードしてインストールするかどうかを指定します。  

    - ソフトウェア更新プログラムのコンテンツが優先配布ポイントにない場合に、クライアントでソフトウェア更新プログラムを代替の配布ポイントからダウンロードしてインストールするかどうかを指定します。  

    - **同じサブネットにある他のクライアントとのコンテンツの共有を許可する**: コンテンツのダウンロードで BranchCache の使用を有効にするかどうかを指定します。 BranchCache について詳しくは、「[コンテンツ管理の基本的な概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)」を参照してください。  

    - **If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates \(現在、近隣、またはサイト グループの配布ポイントでソフトウェア更新プログラムを利用できない場合は、Microsoft 更新プログラムからコンテンツをダウンロードします\)**: 配布ポイントでソフトウェア更新プログラムを利用できない場合に、イントラネットに接続されているクライアントで Microsoft 更新プログラムからソフトウェア更新プログラムをダウンロードする場合は、この設定を選択します。 インターネット ベースのクライアントは、ソフトウェア更新プログラムのコンテンツを取得するために Microsoft 更新プログラムにいつでも移動することができます。

    - クライアントで従量制のインターネット接続を使用している場合に、インストール期限後にクライアントでのダウンロードを許可するかどうかを指定します。 インターネット プロバイダーは、従量制インターネット接続を使用しているときに送受信したデータ量に基づいて課金することがあります。  

    > [!NOTE]  
    >  クライアントは、展開のソフトウェア更新プログラムの管理ポイントからコンテンツの場所を要求します。 ダウンロードの動作は、配布ポイント、展開パッケージ、このページの設定の構成によって異なります。 詳細については、「 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)」をご覧ください。  

11. 「 [手順 3: ソフトウェア更新プログラム グループのコンテンツをダウンロードする](#BKMK_3DownloadContent)」を実行している場合、[展開パッケージ]、[配布ポイント]、[言語の選択] の各ページは表示されず、ウィザードの手順 15 に進むことができます。  

    > [!IMPORTANT]  
    >  サイト サーバーのコンテンツ ライブラリに事前にダウンロードしたソフトウェア更新プログラムは、再度ダウンロードされません。 ソフトウェア更新プログラムの新しい展開パッケージを作成した場合でも同様です。 すべてのソフトウェア更新プログラムが既にダウンロードされている場合、ウィザードは [言語の選択 **** ] ページ (手順 15) に進みます。  

12. [展開パッケージ] ページで、既存の展開パッケージを選択するか、または、次の設定を構成して新しい展開パッケージを指定します。  

    1.  **名前**: 展開パッケージの名前を指定します。 これは、パッケージの内容を説明する一意の名前にする必要があります。 使用できる文字数は最大で 50 文字です。  

    2.  **説明**: 展開パッケージに関する情報を示す説明を指定します。 説明に使用できる文字数は、最大で 127 文字です。  

    3.  **パッケージ ソース**: ソフトウェア更新プログラムのソース ファイルの場所を指定します。  ソースの場所に対応するネットワーク パス (例: **\\\server\sharename\path**) を入力するか、 **[参照]** をクリックして、該当するネットワークの場所を見つけます。 次のページに進む前に、展開パッケージのソース ファイル用の共有フォルダーを作成する必要があります。  

        > [!NOTE]  
        >  指定する展開パッケージのソースの場所を他のソフトウェア展開パッケージで使用することはできません。  

        > [!IMPORTANT]  
        >  SMS プロバイダー コンピューター アカウントと、ウィザードを実行してソフトウェア更新プログラムをダウンロードするユーザーには、ダウンロード先に対する **書き込み** NTFS アクセス許可が必要です。 ソフトウェア更新プログラムのソース ファイルを攻撃者が改ざんするリスクを減らすため、ダウンロード先へのアクセスを注意深く制限する必要があります。  

        > [!IMPORTANT]  
        >  Configuration Manager によって展開パッケージが作成された後で、展開パッケージのプロパティで、パッケージ ソースの場所を変更できます。 ソースの場所を変更する場合、最初に、元のパッケージ ソースから新しいパッケージ ソースの場所にコンテンツをコピーする必要があります。  

    4.  **送信の優先順位**: 展開パッケージの送信の優先順位を指定します。 Configuration Manager は、展開パッケージを配布ポイントに送信するときに、展開パッケージの送信の優先順位を使用します。 展開パッケージは優先順位に従って送信されます。[高]、[中]、[低] の順です。 パッケージの優先順位が同じ場合は、作成された順に送信されます。 バックログがない場合、パッケージは優先順位に関係なく直ちに処理されます。  

13. [配布ポイント] ページで、ソフトウェア更新ファイルをホストする配布ポイントまたは配布ポイント グループを指定します。 配布ポイントの詳細については、「[配布ポイントの構成](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)」を参照してください。  

14. [ダウンロード先] ページで、ソフトウェア更新ファイルをインターネットとローカル ネットワークのどちらからダウンロードするかを指定します。 次の設定を構成します。  

    -   **インターネットからソフトウェア更新プログラムをダウンロードする**: ソフトウェア更新プログラムを、指定したインターネット上の場所からダウンロードします。 既定では、この設定は有効になっています。  

    -   **ネットワーク上の場所からソフトウェア更新プログラムをダウンロードする**: ソフトウェア更新プログラムを、ローカル フォルダーまたは共有ネットワーク フォルダーからダウンロードします。 ウィザードを実行するコンピューターからインターネットにアクセスできない場合は、この設定が役立ちます。 ソフトウェア更新プログラムは、インターネットにアクセス可能な任意のコンピューターから事前にダウンロードし、後でインストールするときにアクセスするローカル ネットワーク上の場所に保存できます。  

15. [言語の選択] ページで、選択したソフトウェア更新プログラムをダウンロードする言語を選択します。 ソフトウェア更新プログラムは、選択した言語で利用できる場合にのみダウンロードされます。 言語固有でないソフトウェア更新プログラムは、常にダウンロードされます。 既定では、ソフトウェアの更新ポイントのプロパティで構成した言語がウィザードで選択されます。 次のページに進む前に、言語を少なくとも 1 つ選択する必要があります。 ソフトウェア更新プログラムでサポートされていない言語のみを選択した場合、ソフトウェア更新プログラムのダウンロードは失敗します。  

16. [要約] ページで、設定を確認します。 設定を展開テンプレートに保存するには、[テンプレートとして保存 ****] をクリックし、名前を入力してテンプレートに含める設定を選択し、[保存 ****] をクリックします。 構成されている設定を変更するには、関連するウィザード ページをクリックして、設定を変更します。  

    > [!WARNING]  
    >  テンプレート名は、英数字の ASCII 文字と、 **\\** (円記号) または **‘** (一重引用符) で構成されます。  

17. ソフトウェア更新プログラムを展開するには、[次へ **** ] をクリックします。  

 ウィザードを完了すると、Configuration Manager でソフトウェア更新プログラムがサイト サーバーのコンテンツ ライブラリにダウンロードされ、構成済みの配布ポイントに配布されて、ターゲット コレクション内のクライアントにソフトウェア更新プログラム グループが展開されます。 展開プロセスの詳細については、「 [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess)」を参照してください。

## 次のステップ
<a id="next-steps" class="xliff"></a>
[ソフトウェア更新プログラムの監視](monitor-software-updates.md)

