---
title: "コマンド ライン インストール | Microsoft Docs"
description: "さまざまなサイトのインストールで、コマンド プロンプトから System Center Configuration Manager セットアップを実行する方法について説明します。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: 8ff48b08d1abb7481592c0ea076d4efa15c3d8ee
ms.contentlocale: ja-jp
ms.lasthandoff: 06/06/2017

---
# コマンド ラインを使用して System Center Configuration Manager サイトをインストールする
<a id="use-a-command-line-to-install-system-center-configuration-manager-sites" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

 さまざまなサイトのインストールで、コマンド プロンプトから System Center Configuration Manager セットアップを実行できます。

## コマンド ラインでのインストールでサポートされているタスク
<a id="supported-tasks-for-command-line-installations" class="xliff"></a>
 この方法でセットアップを実行する場合、次のサイト インストール タスクとサイト メンテナンス タスクがサポートされます。

-   **コマンド プロンプトから中央管理サイトまたはプライマリ サイトをインストールする**  
  [セットアップのコマンド ライン オプション](../../../../core/servers/deploy/install/command-line-options-for-setup.md)を表示する

-  **中央管理サイトまたはプライマリ サイトで使用する言語を変更する**  
    サイトにインストールされている言語 (モバイル デバイスの言語を含む) をコマンド プロンプトから変更するには、次の操作を実行する必要があります。  

     -   サイト サーバーの **&lt;ConfigMgrInstallationPath\>\Bin\X64** からセットアップを実行します
     -   **/MANAGELANGS** コマンド ライン オプションを使用します
     -   追加または削除する言語を指定した言語スクリプト ファイルを指定します  

    たとえば、次のコマンド構文を使用します: **setupwpf.exe/MANAGELANGS &lt;言語スクリプト ファイル\>**  

    言語スクリプト ファイルを作成するには、「[Command line options to manage languages](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)」(言語を管理するためのコマンド ライン オプション) に記載されている情報を参考にしてください。  

-  **サイトの無人インストールまたはサイトの回復にインストール スクリプト ファイルを使用する**  
    インストール スクリプトを使用してコマンド プロンプトからセットアップを実行し、サイトの無人インストールを実行できます。 また、この方法で、サイトを回復することもできます。    

    セットアップでスクリプトを使用するには:  

    -   コマンド ライン オプション **/SCRIPT** を使用してセットアップを実行し、スクリプト ファイルを指定します。  

    -   スクリプト ファイルは、必要なキーと値を使用して構成する必要があります。  

    中央管理サイトまたはプライマリ サイトの無人インストールの場合は、次のセクションがスクリプト ファイルに含まれている必要があります。  

    -   Identification    
    -   Options    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    サイトを回復するには、スクリプト ファイルの次のセクションも含める必要があります。  

    -   Identification  
    -   復元

詳細については、「[Configuration Manager のサイトの無人回復](/sccm/protect/understand/unattended-recovery)」を参照してください。  

無新インストールのスクリプト ファイルで使用するキーと値の一覧を確認するには、「[Unattended Setup script file keys](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended)」(無人セットアップ スクリプト ファイルのキー) を参照してください。  

## コマンド ライン スクリプト ファイルについて
<a id="about-the-command-line-script-file" class="xliff"></a>  
 Configuration Manager の無人インストールの場合は、コマンド ライン オプション **/SCRIPT** を使用してセットアップを実行し、インストール オプションを含むスクリプト ファイルを指定できます。 この方法では、次のタスクがサポートされています。  

-   中央管理サイトをインストールする  
-   プライマリ サイトをインストールする  
-   Configuration Manager コンソールをインストールする  
-   サイトを回復する  

> [!NOTE]  
>  評価サイトを製品版の Configuration Manager にアップグレードする場合、無人スクリプト ファイルを使用することはできません。  

### CDLatest キー名
<a id="the-cdlatest-key-name" class="xliff"></a>
CD.Latest フォルダーのメディアを使用して、次の 4 つのインストール オプションのスクリプト インストールを実行する場合は、値が **1** の **CDLatest** キーを含める必要があります。
- 新しい中央管理サイトをインストールする
- 新しいプライマリ サイトをインストールする
- 中央管理サイトを回復する
- プライマリ サイトを回復する

この値は、Microsoft ボリューム ライセンス サイトから取得したインストール メディアでは使用できません。
スクリプト ファイルでこのキー名を使用する方法の詳細については、[コマンド ライン オプション](/sccm/core/servers/deploy/install/command-line-options-for-setup)を参照してください。



### スクリプトを作成する
<a id="create-the-script" class="xliff"></a>
[サイトをインストールするためにユーザー インターフェイスを使用してセットアップを実行する](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)と、インストール スクリプトが自動的に作成されます。  ウィザードの **[概要]** ページで設定を確認するときに、次の処理が実行されます。  

-   スクリプト **%TEMP%\ConfigMgrAutoSave.ini**が作成されます。  このファイルは使用する前に名前を変更できますが、.ini ファイル拡張子は保持する必要があります。  
-   無人インストール スクリプトには、ウィザードで選択した設定が含まれています。  
-   スクリプトが作成された後、そのスクリプトを変更して、階層に別のサイトをインストールできます。  
-   このスクリプトを使用して、Configuration Manager の無人セットアップを実行できます。  

このスクリプト ファイルで、セットアップ ウィザードで入力するのと同じ情報を指定します。ただし、既定の設定はありません。   
使用する種類のインストールに適用されるセットアップ キーのすべての値を指定する必要があります。   

セットアップで作成される無人インストール用スクリプトには、セットアップ中に入力したプロダクト キーの値が指定されます。 この値は、有効なプロダクト キーか、評価版の Configuration Manager をインストールする場合は **EVAL** になります。 スクリプト内のプロダクト キーの値は、前提条件チェックを完了できるようにするために指定されます。   

セットアップで実際のサイトのインストールが開始されると、自動的に作成されたスクリプトに再度書き込みが行われ、スクリプトのプロダクト キーの値は消去されます。 新しいサイトの無人インストールでスクリプトを使用する前に、スクリプトを編集して、正しいプロダクト キーを指定するか、評価版の Configuration Manager のインストールを指定できます。  

### セクション名、キー名、値
<a id="section-names-key-names-and-values" class="xliff"></a>
スクリプトは、セクション名、キー名、値で構成します。 次の情報にご注意ください。
-   セクションの必須キーは、スクリプトを記述しているインストールの種類によって異なります。
-   セクション内でのキーの順序、およびファイル内でのセクションの順序は重要ではありません。     
-   キー名の大文字と小文字は区別されません。  
-   キーの値を指定するときは、キー名の後ろに等号 (=) を入力してから、キーの値を続けます。    

> [!TIP]  
>  すべてのオプションについては、「[Command-line options for Setup and scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md)」(セットアップのコマンド ライン オプションとスクリプト) を参照してください。  

## /SCRIPT セットアップ コマンドライン オプションを使用する
<a id="use-the-script-setup-command-line-option" class="xliff"></a>

-   セットアップ スクリプト ファイルを使用し、**/SCRIPT** セットアップ コマンド ライン オプションの後にファイル名を指定する必要があります。 次の情報にご注意ください。   
    -   ファイルの名前には、ファイル名拡張子 **.ini** が含まれている必要があります。  
    -   コマンド プロンプトでセットアップ スクリプト ファイルを指定するときは、ファイルの完全パスを入力する必要があります。 たとえば、C:\Setup フォルダーにある Setup.ini というセットアップ初期化ファイルの場合は、コマンド プロンプトに次のように入力します。 **setup /script c:\setup\setup.ini**  

-   セットアップを実行するアカウントには、コンピューターの**管理者**の権限が必要です。 無人インストールを使用してセットアップを実行する場合は、[**管理者として実行**] を使用してコマンド プロンプト ウィンドウを開いてください。   

