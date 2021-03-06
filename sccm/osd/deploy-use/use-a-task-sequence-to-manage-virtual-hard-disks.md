---
title: "バーチャル ハード ディスクを管理するためのタスク シーケンスの使用 | Microsoft Docs"
description: "Configuration Manager から VHD を作成および変更し、アプリケーションとソフトウェア更新プログラムを追加して、VHD を System Center Virtual Machine Manager (VMM) に発行します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: f77af4b8fcb193ed44511c0e5eea7290f55dbbf8


---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>タスク シーケンスによる System Center Configuration Manager でのバーチャル ハード ディスクの管理

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、Configuration Manager コンソールから、バーチャル ハード ディスク (VHD) を管理し、作成した VHD をデータセンターに統合できます。 具体的には、Configuration Manager コンソールから VHD を作成および変更し、アプリケーションとソフトウェア更新プログラムを VHD に追加して、VHD を System Center Virtual Machine Manager (VMM) に発行することができます。  

 次の手順に従って、Configuration Manager で VHD を管理します。

## <a name="prerequisites"></a>必要条件  
 開始する前に、次の前提条件を確認します。  

-   VHD を管理するコンピューターは、次のオペレーティング システムのいずれかを実行する必要があります。  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   BIOS で仮想化を有効にし、Configuration Manager コンソールを実行して VHD を管理するコンピューターに Hyper-V をインストールする必要があります。 また、ベスト プラクティスとして、バーチャル ハード ディスクをテストし、問題を解決しやすくするために、Hyper-V 管理ツールを使用することをおすすめします。 たとえば、smsts.log ファイルを監視して Hyper-V のタスク シーケンスの進行状況を追跡するには、Hyper-V 管理ツールをインストールする必要があります。 Hyper-V の要件の詳細については、「 [Hyper-V をインストールするための前提条件](http://technet.microsoft.com/library/cc731898.aspx)」を参照してください。  

    > [!IMPORTANT]  
    >  VHD を作成するプロセスにはプロセッサの時間とメモリが消費されます。 そのため、サイト サーバーにインストールされていない Configuration Manager コンソールから、VHD を管理することが推奨されます。  

-   サイト サーバーからリモート コンピューターの VHD を管理するときに、サイト サーバーには VHD ファイルを含むフォルダーに対する [書き込み **** ] アクセス許可が必要です。  

-   VHD を管理するコンピューターに、十分な空きディスク領域があることを確認します。 VHD のハード ディスク領域の要件は、インストールするオペレーティング システムとアプリケーションによって異なります。  

-   VHD を管理するコンピューターに十分なメモリがあることを確認してください。 VHD を作成するプロセスでは、2 GB のメモリを消費するようにバーチャル マシンが構成されています。  

-   VHD を VMM にアップロードするコンピューターに、System Center Virtual Machine Manager (VMM) コンソールをインストールします。 VHD を管理するコンピューターとは別のコンピューターに VMM コンソールをインストールできます。つまり、VHD を VMM にインポートするために、Hyper-V をインストールする必要はありません。  

    > [!NOTE]  
    >  Configuration Manager コンソールが開いているときに VMM コンソールをインストールした場合、VMM コンソールのインストールが完了した後に、Configuration Manager コンソールを再起動する必要があります。 そうしないと、Configuration Manager は正常に VMM 管理サーバーに接続して VHD をアップロードすることができません。  

##  <a name="a-namebkmkcreatevhdstepsa-steps-to-create-a-vhd"></a><a name="BKMK_CreateVHDSteps"></a> VHD を作成する手順  
 VHD を作成するには、まず、VHD を作成するタスク シーケンスを作成してから、バーチャル ハード ディスクの作成ウィザードで、そのタスク シーケンスを使います。 次に、その手順を詳しく説明します。  

###  <a name="a-namebkmkcreatetsa-create-a-task-sequence-for-the-vhd"></a><a name="BKMK_CreateTS"></a> VHD のタスク シーケンスを作成する  
 VHD を作成するステップを含むタスク シーケンスを作成する必要があります。 タスク シーケンスの作成ウィザードには、VHD の作成に使用するステップを作成する [既存のイメージ パッケージをバーチャル ハード ディスクにインストールする **** ] オプションがあります。 たとえば、[Windows PE での再起動]、[ディスクのフォーマットとパーティション作成]、[オペレーティング システムの適用]、および [コンピューターのシャットダウン] の必要なステップが追加されます。 フルバージョンのオペレーティング システムでは、VHD を作成できません。 また、Configuration Manager は、バーチャル マシンをシャットダウンしてからパッケージを完了するまで待つ必要があります。 ウィザードの既定では、バーチャル マシンをシャットダウンするまで 5 分間待ちます。 タスク シーケンスの作成後は、必要に応じてステップを追加することができます。  

> [!IMPORTANT]  
>  次の手順では、[既存のイメージ パッケージをバーチャル ハード ディスクにインストールする **** ] オプションを使用してタスク シーケンスを作成します。その結果、VHD を正常に作成するために必要なステップが自動的に含まれます。 既存のタスク シーケンスを使用する場合、または手動でタスク シーケンスを作成する場合、タスク シーケンスの終了時に [コンピューターのシャットダウン] ステップを追加してください。 このステップがない場合、一時的なバーチャル マシンは削除されず、VHD を作成するプロセスは完了しません。 ただし、ウィザードは完了し、成功とレポートされます。  

 次の手順に従って、VHD を作成するタスク シーケンスを作成します。  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>VHD を作成するタスク シーケンスを作成するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ **ソフトウェア ライブラリ** ] ワークスペースで [ **オペレーティング システム**] を展開して、[ **タスク シーケンス**] をクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで [タスク シーケンスの作成 **** ] をクリックして、タスク シーケンスの作成ウィザードを起動します。  

4.  [新しいタスク シーケンスの作成 **** ] ページで、[既存のイメージ パッケージをバーチャル ハード ディスクにインストールする ****] をクリックしてから、[次へ ****] をクリックします。  

5.  [タスク シーケンス情報 **** ] ページで次の設定を指定し、[次へ ****] をクリックします。  

    -   **タスク シーケンス名**:タスク シーケンスを識別する名前を指定します。  

    -   **説明**: タスク シーケンスの説明を指定します。  

    -   **ブート イメージ**:展開先コンピューターにオペレーティング システムをインストールするブート イメージを指定します。 詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

6.  [Windows のインストール] **** ページで次の設定を指定し、[次へ] ****をクリックします。  

    -   **イメージ パッケージ**: インストールするオペレーティング システムを含むパッケージを指定します。  

    -   **イメージ**: オペレーティング システム イメージ パッケージに複数のイメージがある場合は、インストールするオペレーティング システム イメージのインデックスを指定します。  

    -   **プロダクト キー**: インストールする Windows オペレーティング システムのプロダクト キーを指定します。 エンコードされたボリューム ライセンス キーと標準のプロダクト キーを指定できます。 エンコードされていないプロダクト キーを使用する場合は、5 桁ごとにハイフン (-) で区切る必要があります。 例: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **サーバー ライセンス モード**: サーバー ライセンスが **[接続クライアント数]**と **[同時使用ユーザー数]**のいずれか、または決められていないかを指定します。 サーバー ライセンスが [同時使用ユーザー数] ****の場合は、サーバー接続の最大数も指定します。  

    -   オペレーティング システム イメージが展開されたときに使用される管理者アカウントの処理方法を指定します。  

        -   **ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする (推奨)**: この設定を使用すると、ローカル管理者アカウントのパスワードがウィザードによってランダムに生成され、オペレーティング システム イメージを展開するときにアカウントが無効になります。  

        -   **アカウントを有効にし、ローカル管理者パスワードを指定する**: この設定を使用すると、オペレーティング システム イメージが展開されたすべてのコンピューターでローカルの管理者アカウントに特定のパスワードが使用されます。  

7.  [ネットワーク の構成] **** ページで次の設定を指定してから、[次へ] ****をクリックします。  

    -   **ワークグループに参加**:展開先コンピューターをワークグループに追加するかどうかを指定します。  

    -   **ドメインに参加**:展開先コンピューターをドメインに追加するかどうかを指定します。 [ドメイン] ****にドメインの名前を指定します。  

        > [!IMPORTANT]  
        >  ローカル フォレストではドメインを参照できますが、リモート フォレストではドメイン名を指定する必要があります。  

         組織単位 (OU) も指定することができます。 OU の LDAP X.500 識別名を指定するオプションの設定です。コンピューター アカウントがまだ存在しない場合に作成するのに使用されます。  

    -   **アカウント**: 指定したドメインに参加するアクセス許可を持つアカウントの、ユーザー名とパスワードを指定します。 例: *domain\user* または *%variable%*。  

8.  [**Configuration Manager のインストール**] ページで、インストール先コンピューターにインストールする Configuration Manager クライアント パッケージを指定してから、[**次へ**] をクリックします。  

9. [アプリケーションのインストール] **** ページで、展開先コンピューターにインストールするアプリケーションを指定してから、[次へ] ****をクリックします。 複数のアプリケーションを指定する場合は、特定のアプリケーションのインストールに失敗したときにタスク シーケンスを続行するかどうかも指定することができます。  

10. ウィザードを完了します。  

###  <a name="a-namebkmkcreatevhda-create-a-vhd"></a><a name="BKMK_CreateVHD"></a> VHD を作成する  
 VHD 作成用のタスク シーケンスを作成したら、バーチャル ハード ディスクの作成ウィザードを使用して VHD を作成します。  

> [!IMPORTANT]  
>  この手順を実行する前に、このトピックの冒頭に記載されている前提条件を満たすことを確認します。  

 次の手順に従って、VHD を作成します。  

#### <a name="to-create-a-vhd"></a>VHD を作成するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ **** ] ワークスペースで [オペレーティング システム ****] を展開して、[バーチャル ハード ディスク ****] をクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[バーチャル ハード ディスクの作成 **** ] をクリックして、バーチャル ハード ディスクの作成ウィザードを開始します。  

    > [!NOTE]  
    >  VHD を管理している、または [**バーチャル ハード ディスクの作成**] オプションが有効になっていない Configuration Manager コンソールを実行しているコンピューターに、Hyper-V をインストールする必要があります。 Hyper-V の要件の詳細については、「 [Hyper-V をインストールするための前提条件](http://technet.microsoft.com/library/cc731898.aspx)」を参照してください。  

    > [!TIP]  
    >  VHD を整理するために、[バーチャル ハード ディスク **** ] ノード以下に新しいフォルダーを作成するか、既存のフォルダーを選択して、フォルダーから [バーチャル ハード ディスクの作成 **** ] をクリックします。  

4.  [全般 **** ] ページで、次の設定を指定して [次へ ****] をクリックします。  

    -   **名前**: VHD 固有の名前を指定します。  

    -   **バージョン**: VHD のバージョン番号を指定します。 この設定は省略可能です。  

    -   **コメント**: VHD の説明を指定します。  

    -   **パス**: ウィザードが VHD ファイルを作成する場所のパスとファイル名を指定します。  

         UNC 形式で有効なネットワーク パスを入力する必要があります。 例: **\\\servername\\<sharename\>\\<filename\>.vhd**  

        > [!WARNING]  
        >  VHD を作成するために、Configuration Manager には指定されたパスへの**書き込み**アクセス許可が必要です。 Configuration Manager がこのパスへのアクセスに失敗すると、サイト サーバーの distmgr.log ファイルに関連するエラーが記録されます。  

5.  [タスク シーケンスの選択 **** ] ページで、前のセクションで指定したタスク シーケンスを選択し、[次へ ****] をクリックします。  

6.  [配布ポイント **** ] ページで、タスク シーケンスに必要なコンテンツがある配布ポイントを 1 つまたは複数選択し、[次へ ****] をクリックします。  

7.  **[カスタマイズ]** ページで、 **[次へ]**をクリックします。 このページで何か設定しても、VHD を作成するプロセスによって無視されます。  

8.  設定を確認し、[次へ ****] をクリックします。 VHD が作成されます。  

    > [!TIP]  
    >  VHD を作成するプロセスが完了するまでにかかる時間は変わる可能性があります。 ウィザードがこのプロセスを実行しているときに、次のログ ファイルで、進行状況を追跡することができます。 ログは、既定で、Configuration Manager コンソールを実行するコンピューターの %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog にあります。  
    >   
    >  -   **CreateTSMedia.log**: ウィザードでタスク シーケンス メディアの作成時に、このログに情報が書き込まれます。 スタンドアロン メディアを作成するときは、このログ ファイルを確認して、ウィザードの進行状況を追跡します。  
    > -   **DeployToVHD.log**: VHD を作成するプロセスの実行中に、このログに情報が書き込まれます。 スタンドアロン メディアを作成したら、すべてのステップについてこのログ ファイルを確認して、ウィザードの進行状況を追跡します。  
    >   
    >  また、オペレーティング システムのインストールが起動するときに、Hyper-V マネージャーを開き (Hyper-V 管理ツールをコンピューターにインストールした場合)、ウィザードによって作成された一時的なバーチャル マシンに接続して、実行しているタスク シーケンスを確認できます。 バーチャル マシンから、smsts.log ファイルを監視して、タスク シーケンスの進行状況を追跡できます。 問題があってタスク シーケンスのステップを完了できない場合、このログ ファイルを使用して問題を解決できます。 smsts.log ファイルは、ハード ディスクをフォーマットする前は x: \windows\temp\smstslog\smsts.log にあり、フォーマット後は c:\\_SMSTaskSequence\Logs\Smstslog\ にあります。 タスク シーケンスのステップが完了したら、5 分間 (既定) 経った後にバーチャル マシンがシャットダウンされ、削除されます。  

 Configuration Manager が VHD を作成した後、VHD は [**ソフトウェア ライブラリ**] ワークスペースの [**オペレーティング システムの展開**] の下にある Configuration Manager コンソールの [**仮想ハード ドライブ**] ノードに配置されます。  

> [!NOTE]  
>  Configuration Manager が、VHD のソースの場所に接続して、VHD のサイズを取得します。 Configuration Manager が VHD ファイルにアクセスできない場合、VHD の [**サイズ (KB)**] 列に "**0**" が表示されます。  

##  <a name="a-namebkmkmodifyvhdstepsa-steps-to-modify-an-existing-vhd"></a><a name="BKMK_ModifyVHDSteps"></a> 既存の VHD を変更する手順  
 VHD を変更するには、まず、VHD を変更するのに必要なステップを含むタスク シーケンスを作成します。 次に、バーチャル ハード ディスクの変更ウィザードで、そのタスク シーケンスを選択します。 VHD がバーチャル マシンにアタッチされ、VHD でタスク シーケンスが実行されて、VHD ファイルが変更されます。 次に、その手順を詳しく説明します。  

###  <a name="a-namebkmkmodifytsa-create-a-task-sequence-to-modify-the-vhd"></a><a name="BKMK_ModifyTS"></a> VHD を変更するタスク シーケンスを作成する  
 既存の VHD を変更するには、まず、タスク シーケンスを作成する必要があります。 次に、このタスク シーケンスを変更するのに必要なステップだけを選択します。 たとえば、VHD にアプリケーションを追加したい場合は、タスク シーケンスを作成してから、[アプリケーションのインストール] ステップだけを追加します。  

 VHD を変更するタスク シーケンスを作成するには、次の手順に従います。  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>VHD を変更するタスク シーケンスを作成するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ **ソフトウェア ライブラリ** ] ワークスペースで [ **オペレーティング システム**] を展開して、[ **タスク シーケンス**] をクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで [タスク シーケンスの作成 **** ] をクリックして、タスク シーケンスの作成ウィザードを起動します。  

4.  **[新しいタスク シーケンスの作成]** ページで **[新しいカスタム タスク シーケンスを作成する]**を選択し、 **[次へ]**をクリックします。  

5.  [タスク シーケンス情報 **** ] ページで次の設定を指定し、[次へ ****] をクリックします。  

    -   **タスク シーケンス名**:タスク シーケンスを識別する名前を指定します。  

    -   **説明**: タスク シーケンスの説明を指定します。  

    -   **ブート イメージ**:展開先コンピューターにオペレーティング システムをインストールするブート イメージを指定します。 詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

6.  ウィザードを完了します。  

 カスタム タスク シーケンスにステップを追加するには、次の手順に従います。  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>カスタム タスク シーケンスにステップを追加するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ] **** ワークスペースの [オペレーティング システム] ****を展開して [タスク シーケンス] ****をクリックし、前の手順で作成したカスタム タスク シーケンスを選択します。  

3.  [ホーム **** ] タブの [タスク シーケンス **** ] グループの [編集 **** ] をクリックし、タスク シーケンス エディターを開きます。  

4.  VHD を変更するステップを追加します。  

5.  [OK] をクリックして、タスク シーケンス エディターを閉じます。 ****  

###  <a name="a-namebkmkmodifyvhda-modify-a-vhd"></a><a name="BKMK_ModifyVHD"></a> VHD を変更する  
 VHD 変更用のタスク シーケンスを作成したら、バーチャル ハード ディスクの変更ウィザードを使用して VHD を変更します。  

 VHD を変更するには、次の手順に従います。  

#### <a name="to-modify-a-vhd"></a>VHD を変更するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ **** ] ワークスペースの [オペレーティング システム ****] を展開して [バーチャル ハード ディスク ****] をクリックし、変更する VHD を選択します。  

3.  [ホーム **** ] タブの [バーチャル ハード ディスク **** ] グループの [バーチャル ハード ディスクの変更 **** ] をクリックし、バーチャル ハード ディスクの変更ウィザードを開始します。  

    > [!NOTE]  
    >  VHD を管理している、または [**バーチャル ハード ディスクの変更**] オプションが有効になっていない Configuration Manager コンソールを実行しているコンピューターに、Hyper-V をインストールする必要があります。 Hyper-V の要件の詳細については、「 [Hyper-V をインストールするための前提条件](http://technet.microsoft.com/library/cc731898.aspx)」を参照してください。  

4.  [全般 **** ] ページで、次の設定を確認して [次へ ****] をクリックします。  

    -   **名前**: VHD 固有の名前を指定します。  

    -   **バージョン**: VHD のバージョン番号を指定します。 この設定は省略可能です。  

    -   **コメント**: VHD の説明を指定します。  

    -   **パス**: VHD ファイルのパスとファイル名を指定します。 この設定は変更できません。  

        > [!WARNING]  
        >  VHD を作成するために、Configuration Manager には指定されたパスへの**書き込み**アクセス許可が必要です。 Configuration Manager がこのパスへのアクセスに失敗すると、サイト サーバーの distmgr.log ファイルに関連するエラーが記録されます。  

5.  [タスク シーケンスの選択 **** ] ページで、前のセクションで作成したカスタム タスク シーケンスを指定して [次へ ****] をクリックします。  

6.  [配布ポイント **** ] ページで、タスク シーケンスに必要なコンテンツがある配布ポイントを 1 つまたは複数選択し、[次へ ****] をクリックします。  

7.  **[カスタマイズ]** ページで、 **[次へ]**をクリックします。 このページで何か設定しても、VHD を変更するプロセスによって無視されます。  

8.  設定を確認し、[次へ ****] をクリックします。 VHD が変更されます。  

    > [!TIP]  
    >  VHD の変更が完了するまでの時間は、状況によって異なります。 ウィザードがこのプロセスを実行しているときに、次のログ ファイルで、進行状況を追跡することができます。 ログは、既定で、Configuration Manager コンソールを実行するコンピューターの %*ProgramFiles(x86)*%\Microsoft Configuration Manager\AdminConsole\AdminUILog にあります。  
    >   
    >  -   **CreateTSMedia.log**: ウィザードでタスク シーケンス メディアの作成時に、このログに情報が書き込まれます。 スタンドアロン メディアを作成するときは、このログ ファイルを確認して、ウィザードの進行状況を追跡します。  
    > -   **DeployToVHD.log**: VHD を変更するプロセスの実行中に、このログに情報が書き込まれます。 スタンドアロン メディアを作成したら、すべてのステップについてこのログ ファイルを確認して、ウィザードの進行状況を追跡します。  
    >   
    >  また、Hyper-V マネージャーを開き (Hyper-V 管理ツールをコンピューターにインストール済みの場合)、ウィザードによって作成された一時的なバーチャル マシンに接続して、実行されているタスク シーケンスを確認できます。 バーチャル マシンから、smsts.log ファイルを監視して、タスク シーケンスの進行状況を追跡できます。 問題があってタスク シーケンスのステップを完了できない場合、このログ ファイルを使用して問題を解決できます。 smsts.log ファイルは、ハード ディスクをフォーマットする前は x: \windows\temp\smstslog\smsts.log にあり、フォーマット後は c:\\_SMSTaskSequence\Logs\Smstslog\ にあります。 タスク シーケンスのステップが完了したら、5 分間 (既定) 経った後にバーチャル マシンがシャットダウンされ、削除されます。  

##  <a name="a-namebkmkapplyupdatesa-apply-software-updates-to-a-vhd"></a><a name="BKMK_ApplyUpdates"></a> ソフトウェア更新プログラムを VHD に適用する  
 使用している VHD のオペレーティング システムに適用できる新しいソフトウェア更新プログラムは、定期的にリリースされます。 適用できるソフトウェア更新プログラムは、指定したスケジュールで VHD に適用できます。 Configuration Manager は、指定するスケジュールで、選択したソフトウェア更新プログラムを VHD に適用します。  

 VHD の作成時点で適用されたソフトウェア更新プログラムなど、VHD に関する情報はサイト データベースに保管されます。 最初の作成以降、VHD に適用されたソフトウェア更新プログラムもサイト データベースに保管されます。 ソフトウェア更新プログラムを VHD に適用するウィザードを開始すると、その VHD にまだ適用していない適用可能なソフトウェア更新プログラムの一覧が選択対象として取得されます。  

 選択したソフトウェア更新プログラムの 1 つ以上にエラーが発生しても、[**エラー時に続行する**] 設定を選択して、Configuration Manager がソフトウェア更新プログラムの適用を続行するようにできます。  

> [!NOTE]  
>  ソフトウェア更新プログラムはサイト サーバーのコンテンツ ライブラリからコピーされます。  

 次の手順に従って、ソフトウェア更新プログラムを VHD に適用します。  

#### <a name="to-apply-software-updates-to-a-vhd"></a>ソフトウェア更新プログラムを VHD に適用するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ **** ] ワークスペースで [オペレーティング システム ****] を展開して、[バーチャル ハード ディスク ****] をクリックします。  

3.  ソフトウェア更新プログラムを適用する VHD を選択します。  

4.  [ホーム **** ] タブの [バーチャル ハード ディスク **** ] グループで、[更新のスケジュール **** ] をクリックしてウィザードを開始します。  

5.  [更新プログラムの選択 **** ] ページで、VHD に適用するソフトウェア更新プログラムを選択し、[次へ ****] をクリックします。  

6.  **[スケジュールの設定]** ページで、次の設定を指定して、 **[次へ]**をクリックします。  

    1.  **スケジュール**: ソフトウェア更新プログラムを VHD に適用するスケジュールを指定します。  

    2.  **エラー時に続行する**: このオプションを選択すると、エラーが発生した場合でも、イメージにソフトウェア更新プログラムがそのまま適用されます。  

7.  **[概要]** ページで、情報を確認して **[次へ]**をクリックします。  

8.  [完了] ページで、オペレーティング システム イメージにソフトウェア更新プログラムが正常に適用されたことを確認します。 ****  

##  <a name="a-namebkmkimporttovmma-import-the-vhd-to-system-center-virtual-machine-manager"></a><a name="BKMK_ImportToVMM"></a> VHD を System Center Virtual Machine Manager にインポートする  
 System Center VMM は、仮想化されたデータセンターの管理ソリューションです。仮想化ホスト、ネットワーキング、および記憶域リソースを構成および管理できます。バーチャル マシンとサービスを作成して、作成したプライベート クラウドに展開することができます。 Configuration Manager で VHD を作成したら、VMM を使用して VHD をインポートおよび管理できます。  

> [!TIP]  
>  VHD を VMM にアップロードする前に、VMM コンソールが VMM 管理サーバーに正常に接続していることを確認します。  

 次の手順に従って、VHD を VMM にインポートします。  

#### <a name="to-import-a-vhd-to-vmm"></a>VHD を VMM にインポートするには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ソフトウェア ライブラリ **** ] ワークスペースで [オペレーティング システム ****] を展開して、[バーチャル ハード ディスク ****] をクリックします。  

3.  [ホーム **** ] タブの [バーチャル ハード ディスク **** ] グループで、[Virtual Machine Manager にアップロード **** ] を Virtual Machine Manager にアップロード ウィザードを開始します。  

4.  [全般 **** ] ページで、次の設定を構成してから、[次へ ****] をクリックします。  

    -   **VMM サーバー名**: VMM 管理サーバーをインストールするコンピューターの FQDN を指定します。 VMM 管理サーバーに接続され、サーバーのライブラリ共有がダウンロードされます。  

    -   **VMM ライブラリ共有**: ドロップダウン リストから VMM ライブラリ共有を指定します。  

    -   **暗号化されていない転送を使用する**: 暗号化を使用せずに、VHD ファイルを VMM 管理サーバーに転送するには、この設定を選択します。  

5.  [概要] ページで設定を確認し、ウィザードを完了します。 VHD のアップロードにかかる時間は、VHD ファイルのサイズと、VMM 管理サーバーに対するネットワーク帯域幅によって変わります。  



<!--HONumber=Dec16_HO3-->


