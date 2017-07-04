---
title: "Office 365 ProPlus 更新プログラムの管理 | Microsoft Docs"
description: "Configuration Manager が WSUS カタログからサイト サーバーに Office 365 のクライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 016580dc6ee3c5268833db941d42416a976d201c
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Configuration Manager での Office 365 ProPlus の管理

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager は Office 365 クライアントの更新プログラムと同期しており、この更新プログラムを、Office 365 がインストールされているクライアントに展開することができます。 Configuration Manager バージョン 1610 以降では、Office 365 クライアント管理ダッシュボードから Office 365 クライアントの情報を確認できます。

Configuration Manager バージョン 1602 以降では、ソフトウェア更新管理のワークフローを使用して、Office 365 クライアントの更新プログラムを管理できます。 マイクロソフトが Office コンテンツ配信ネットワーク (CDN) に対する新しい Office 365 のクライアント更新プログラムを公開するときには、Windows Server Update Services (WSUS) に対する更新パッケージも公開します。 Configuration Manager が WSUS カタログからサイト サーバーに Office 365 クライアント更新プログラムを同期したら、その更新プログラムをクライアントに展開できるようになります。

バージョン 1702 以降では、Office 365 クライアント管理ダッシュボードから Office 365 インストーラーを起動することで、最初の Office 365 アプリのインストール操作をより簡単にすることができます。 ウィザードに従って、Office 365 のインストール設定を構成し、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードして、コンテンツを含むスクリプト アプリケーションを作成して展開することができます。

## <a name="office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボード  
Configuration Manager バージョン 1610 より、Office 365 クライアント管理ダッシュボードを Configuration Manager コンソールで利用できます。 このダッシュボードを表示するには、**[ソフトウェア ライブラリ]** > **[概要]** > **[Office 365 クライアント管理]** に移動します。

ダッシュボードには、次のチャートが表示されます。

- Office 365 クライアントの数
- Office 365 クライアントのバージョン
- Office 365 クライアントの言語
- Office 365 クライアントのチャネル     
詳細については、「[Office 365 ProPlus 更新プログラム チャネルの概要](https://technet.microsoft.com/library/mt455210.aspx)」をご覧ください。
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

ダッシュボードの上部にある [**コレクション**] ドロップダウン設定を使用して、特定のコレクションのメンバーでダッシュボードのデータをフィルター処理します。

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボードにデータを表示する
Office 365 クライアント管理ダッシュ ボードに表示されるデータは、ハードウェア インベントリから取得されます。 データがダッシュボードに表示される前に、ハードウェア インベントリを有効にし、**Office 365 ProPlus 構成**ハードウェア インベントリ クラスを選択する必要があります。
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボードにデータを表示するには
1. ハードウェア インベントリがまだ有効になっていない場合は、有効にします。 詳細については、「[Configure hardware inventory](\sccm\core\clients\manage\configure-hardware-inventory)」(ハードウェア インベントリを構成する) を参照してください。
2. Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  
3. **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  
4. [ **既定のクライアント設定** ] ダイアログ ボックスで、[ **ハードウェア インベントリ** ] をクリックします。  
5. [ **デバイス設定** ] の一覧で、[ **クラスの設定** ] をクリックします。  
6. **[ハードウェア インベントリ クラス]** ダイアログ ボックスで、**[Office 365 ProPlus 構成]** を選択します。  
7.  [ **OK** ] をクリックして変更を保存し、[ **ハードウェア インベントリ クラス** ] ダイアログ ボックスを閉じます。  
ハードウェア インベントリが報告されると、Office 365 クライアント管理ダッシュボードにデータが表示されます。

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Configuration Manager で Office 365 の更新プログラムを展開する
Configuration Manager で Office 365 の更新プログラムを展開するには、次の手順を使用します。

1.  Configuration Manager を使用して Office 365 クライアントの更新プログラムを管理するための[要件を確認します](https://technet.microsoft.com/library/mt628083.aspx) (このトピックの「**構成マネージャーを使用して Office 365 クライアントの更新を管理するための要件**」セクションを参照してください)。  

2.  Office 365 のクライアント更新プログラムを同期するための[ソフトウェア更新ポイントを構成します](../get-started/configure-classifications-and-products.md)。 分類の**更新プログラム**を設定して、製品の **Office 365 クライアント**を選択します。 Office 365 クライアント製品を選択できるようになるには、ソフトウェア更新プログラムを少なくとも 1 回同期しておく必要があります。 分類の**更新プログラム**を使用するには、ソフトウェア更新ポイントの構成後にソフトウェア更新プログラムを同期する必要があります。
3.  Office 365 クライアントが Configuration Manager から更新プログラムを受信できるようにします。 そのためには、Configuration Manager クライアント設定またはグループ ポリシーを使用します。 次のいずれかの方法を使用してクライアントを有効にします。  
    - 方法 1: Configuration Manager バージョン 1606 以降では、Configuration Manager クライアント設定を使用して Office 365 のクライアント エージェントを管理できます。 この設定を構成し、Office 365 の更新プログラムを展開すると、Configuration Manager クライアント エージェントは、Office 365 のクライアント エージェントと通信して、配布ポイントから Office 365 の更新プログラムをダウンロードしてインストールします。 Configuration Manager は、Office 365 ProPlus クライアント エージェント設定のインベントリを取得します。
      1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クライアント設定]** の順にクリックします。  

      2.  クライアント エージェントを有効にする適切なデバイスの設定を開きます。 既定およびカスタムのクライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

      3.  **[ソフトウェアの更新]** を選択し、**[Office 365 クライアント エージェントの管理を有効にする]** の設定に **[はい]** を設定します。  

    - 方法 2: Office 展開ツールまたはグループ ポリシーを使用して、Configuration Manager から [Office 365 クライアントが更新プログラムを受信できるようにします](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient)。  

4. [Office 365 の更新プログラムをクライアントに展開します](deploy-software-updates.md)。   

> [!Important]
> Office 365 クライアントに複数の言語を設定している状態で、その言語数より少ない言語用の更新プログラムをダウンロードした場合、インストールは失敗します。 たとえば、Office 365 クライアントに en-us と de-de を設定しているとします。 サイト サーバーで、適用可能な Office 365 更新プログラムに対して en-us のコンテンツのみをダウンロードして展開します。 ユーザーがソフトウェア センターからこの更新プログラムのインストールを開始すると、更新プログラムはコンテンツのダウンロード中にハングします。 Office 365 クライアントと同じ言語の更新プログラムをダウンロードして展開する必要があります。  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Office 365 更新プログラムのダウンロード対象言語を追加する
バージョン 1610 以降の Configuration Manager では、Office 365 でサポートされている言語であれば、Configuration Manager でサポートされているかどうかに関係なく、その言語の更新プログラムをダウンロード対象に含めることができます。
> [!IMPORTANT]  
> Office 365 更新プログラムの言語を追加するための構成設定はサイト全体に適用されます。 以下の手順に従って言語を追加すると、その言語における Office 365 のすべての更新プログラムが、ソフトウェア更新プログラムの展開ウィザードまたはソフトウェア更新プログラムのダウンロード ウィザードの [言語の選択] ページで選択した言語に加えてダウンロードされます。

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>更新プログラムのダウンロード対象言語を追加するには
以下の手順は、ソフトウェアの更新ポイント サイト システムの役割がインストールされている中央管理サイト (またはスタンドアロンのプライマリ サイト) で実行してください。
1. 管理ユーザーとしてコマンド プロンプトから「*wbemtest*」と入力し、Windows Management Instrumentation テストを開きます。
2. **[接続]** をクリックして「*root\sms\site_&lt;siteCode&gt;*」と入力します。
3. **[クエリ]** をクリックして、「*select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*」というクエリを実行します。  
   ![WMI query](..\media\1-wmiquery.png)
4. 結果ウィンドウで、目的のサイト コード (中央管理サイトまたはスタンドアロンのプライマリ サイト) に該当するオブジェクトをダブルクリックします。
5. **Props** プロパティを選択し、**[プロパティの編集]** をクリックして、**[埋め込みを表示]** をクリックします。
![Property editor](..\media\2-propeditor.png)
6. 1 つ目のクエリ結果から順に各オブジェクトを開いていき、**PropertyName** プロパティが **AdditionalUpdateLanguagesForO365** であるオブジェクトを見つけます。
7. **[Value2]** を選択し、**[プロパティの編集]** をクリックします。  
![Edit the Value2 property](..\media\3-queryresult.png)
8. 新しい言語を **Value2** プロパティに追加して **[プロパティの保存]** をクリックします。  
たとえば、pt-pt (ポルトガル語 - ポルトガル)、af-za (アフリカーンス語 - 南アフリカ)、nn-no (ノルウェー語 (ニーノシク) - ノルウェー) を追加します。  
![Add languages in Property Editor](..\media\4-props.png)  
9. **[閉じる]** をクリックし、再度 **[閉じる]** をクリックして、**[プロパティの保存]** をクリックし、**[オブジェクトの保存]** (ここで **[閉じる]** をクリックした場合は、値が破棄されます) をクリックします。次に、**[閉じる]** をクリックし、**[終了]** をクリックして、Windows Management Instrumentation テストを終了します。
10. Configuration Manager コンソールで **[ソフトウェア ライブラリ]** > **[概要]** > **[Office 365 クライアント管理]** > **[Office 365 Updates (Office 365 更新プログラム)]** に移動します。
11. 以後、Office 365 更新プログラムをダウンロードすると、ウィザードで選択した言語およびこの手順で構成した言語の更新プログラムがダウンロードされます。 該当する言語の更新プログラムがダウンロードされたことを確認するには、その更新プログラムのパッケージ ソースにアクセスし、対応する言語コードを名前に含んだファイルを探します。  
![Filenames with additional languages](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Configuration Manager から更新プログラムを適用できるように Office 365 クライアントを設定した後で更新チャネルを変更する
Configuration Manager から更新プログラムを適用できるように Office 365 クライアントを設定した後で更新チャネルを変更するには、グループ ポリシーを使用して、レジストリ キー値の変更を Office 365 クライアントに配信します。 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** というレジストリ キーを次のいずれかの値を使用するように変更します。

- 最新機能提供チャネル:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- 段階的提供チャネル:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- 最新機能提供チャネルの初回リリース:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- 段階的提供チャネルの初回リリース:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Office 365 アプリを展開する  
バージョン 1702 以降では、Office 365 クライアント管理ダッシュボードから Office 365 インストーラーを起動して、最初の Office 365 アプリのインストール操作をより簡単にすることができます。 ウィザードに従って、Office 365 のインストール設定を構成し、Office コンテンツ配信ネットワーク (CDN) からファイルをダウンロードして、そのファイルのスクリプト アプリケーションを作成して展開することができます。

Office 365 更新プログラムは Office 365 がインストールされていないクライアントには適用できないため、これは特に便利です。 1702 より前のバージョンでは、クライアントに初めて Office 365 アプリをインストールする場合に、Office 365 Deployment Tool (ODT) と、必要な言語パックをすべて含む Office 365 インストール ソース ファイルを手動でダウンロードし、適切な Office のバージョンとチャネルを指定する Configuration.xml を生成する必要があります。 次に、従来のパッケージ、または Office 365 アプリをインストールするクライアント用のスクリプト アプリケーションを作成して展開する必要があります。

> [!NOTE]
> - Office 365 インストーラーを実行しているコンピューターではインターネット アクセスが必要になります。  
> - Office 365 インストーラーを実行しているユーザーには、ウィザードで示されるコンテンツの場所の共有に対する**読み取り**および**書き込み**アクセス権が必要です。
> - 404 ダウンロード エラーが発生した場合は、次のファイルをユーザーの %temp% フォルダーにコピーします。
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Office 365 インストーラーを使用して Office 365 アプリケーションを作成して展開した場合、既定では Configuration Manage で Office 更新プログラムが管理されません。 Office 365 クライアントで Configuration Manager から更新プログラムを受信できるようにする場合は、「[Configuration Manager で Office 365 の更新プログラムを展開する](#deploy-office-365-updates-with-configuration-manager)」を参照してください。

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Office 365 クライアント管理ダッシュボードからクライアントに Office 365 アプリを展開するには
1. Configuration Manager コンソールで [**ソフトウェア ライブラリ**] > [**概要**] > [**Office 365 クライアント管理**] に移動します。
2. 右上のウィンドウで [**Office 365 インストーラー**] をクリックします。 Office 365 クライアントのインストール ウィザードが開きます。
3. [**アプリケーションの設定**] ページでアプリの名前と説明を入力し、ファイルをダウンロードする場所を入力して、[**次へ**] をクリックします。 場所は &#92;&#92;*server*&#92;*share* の形式で指定する必要があります。
4. [**クライアント設定のインポート**] ページで、Office 365 クライアントの設定を既存の XML 構成ファイルからインポートするか、手動で設定を指定するかどうかを選び、[**次へ**] をクリックします。  

    既存の構成ファイルを使用する場合は、ファイルの場所を入力し、ステップ 7 に進みます。 場所は &#92;&#92;*server*&#92;*share*&#92;*filename*.XML の形式で指定する必要があります。
5. [**クライアント プロダクト**] ページで、使用する Office 365 スイートを選び、含めたいアプリケーションを選び、含める必要がある追加の Office 製品を選び、[**次へ**] をクリックします。
6. [**クライアント設定**] ページで、含める設定を選び、[**次へ**] をクリックします。
7. [**展開**] ページで、アプリケーションを展開するかどうかを選び[**次へ**] をクリックします。  
ウィザードでパッケージを展開しないことを選択した場合は、ステップ 9 に進みます。
8. 一般的なアプリケーション展開の場合と同様に、ウィザードの残りのページを構成します。 詳細については、「[アプリケーションの作成手順と展開手順](/sccm/apps/get-started/create-and-deploy-an-application)」を参照してください。
9. ウィザードを完了します。
10. 他のアプリケーションと同様に、Configuration Manager で [**ソフトウェア ライブラリ**] > [**概要**] > [**アプリケーション管理**] > [**アプリケーション**] の順に選択して、アプリケーションを展開または編集することができます。   

> [!IMPORTANT]
> Configuration Manager で Office 365 アプリケーション ウィザードを使用して作成し、展開した Office 365 は、**[Office 365 クライアント エージェントの管理を有効にする]** ソフトウェア更新プログラム クライアント エージェント設定を有効にしない限り、Configuration Manager で自動的に管理されません。 詳細については、「[System Center Configuration Manager のクライアント設定について](/sccm/core/clients/deploy/about-client-settings)」を参照してください。

>[!NOTE]
>Office 365 アプリを展開すると、アプリを維持するための自動展開規則を作成できます。 Office 365 アプリの自動展開規則を作成するには、Office 365 クライアント管理ダッシュボードから **[ADR の作成]** をクリックし、製品を選択する際に **[Office 365 クライアント]** を選択します。 詳細については、「[ソフトウェア更新プログラムの自動展開](/sccm/sum/deploy-use/automatically-deploy-software-updates)」を参照してください。

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

