---
title: "クエリの作成 | Microsoft Docs"
description: "System Center Configuration Manager でクエリを作成してインポートする方法を紹介します。 クエリの例とヒントが含まれています。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2087badc9dd1d216352dce232b145a786783ac89
ms.openlocfilehash: 9f38d86ff6227bb6ea88c358a3d61242372d449e
ms.contentlocale: ja-jp
ms.lasthandoff: 05/18/2017


---
# System Center Configuration Manager でクエリを作成する方法
<a id="how-to-create-queries-in-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でクエリを作成またはインポートするときは、このトピックを参照してください。  

##  <a name="BKMK_Create"></a> クエリを作成する方法  
 Configuration Manager でクエリを作成するには、この手順に従います。  

#### クエリを作成するには
<a id="to-create-a-query" class="xliff"></a>  

1.  Configuration Manager コンソールで、**[監視]** をクリックします。  

2.  **[監視]** ワークスペースで、**[クエリ]** を選択します。 **[ホーム]** タブの **[作成]** グループで **[クエリの作成]** を選択します。  

3.  **全般** のタブ、 **クエリの作成ウィザード**, 、一意の名前と、クエリのオプションのコメントを指定します。  

4.  既存のクエリをインポートして新しいクエリの基礎として使用するには、**[クエリ ステートメントのインポート]** を選択します。 **[クエリの参照]** ダイアログ ボックスで、インポートする既存のクエリを選択し、**[OK]** を選択します。  

5.  **[オブジェクトの種類]** 一覧で、クエリが返すオブジェクトの種類を選択します。 次の表に、検索可能なオブジェクトの種類の例をいくつか示します。  

    |オブジェクトの種類|説明|  
    |-----------------|-----------------|  
    |**[システム リソース]**|デバイスの NetBIOS 名、クライアントのバージョン、クライアントの IP アドレス、Active Directory ドメイン サービス情報など、一般的なシステム属性の検索に使用します。|  
    |**[ユーザー リソース]**|ユーザー名、ユーザー グループ名、セキュリティ グループ名など、一般的なユーザー情報の検索に使用します。|  
    |**展開**|展開名、スケジュール、展開先となったコレクションなど、展開の一般的な属性の検索に使用します。|  

6.  **[クエリ ステートメントの編集]** を選択して、*[&lt;クエリ名\>* **ステートメントのプロパティ]** ダイアログ ボックスを開きます。  

7.  *[&lt;クエリ名\>* **ステートメントのプロパティ]** ダイアログ ボックスの **[全般]** タブで、クエリが返す属性と、その属性の表示方法を指定します。 **[新規]** アイコンをクリックして、新しい属性を追加します。 **[クエリ言語を表示する]** を選択して、クエリを、直接 WMI クエリ言語 (WQL) で入力または編集することもできます。 WMI クエリの例については、このトピックの「 [Example WQL queries](#BKMK_Example) 」セクションを参照してください。  

    > [!TIP]  
    > 独自の WQL クエリを作成する場合は、次の MSDN リファレンス ドキュメントを参考にしてください。  
    >   
    > -   [WQL (WMI 用の SQL)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE 句](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL オペレーター](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  *[&lt;クエリ名\>* **ステートメントのプロパティ]** ダイアログ ボックスの **[条件]** タブで、クエリ結果の絞り込みに使用する条件を指定します。 たとえば、クエリ結果にサイト コード **XYZ** を含むリソースのみを返すことができます。 1 つのクエリに複数の条件を構成することができます。  

    > [!IMPORTANT]  
    > 条件が含まれないクエリを作成した場合、そのクエリは、 **[すべてのシステム]** コレクションのすべてのデバイスを返します。  

9. *[&lt;クエリ名\>* **ステートメントのプロパティ]** ダイアログ ボックスの **[結合]** タブで、2 つの異なる属性からのデータをクエリ結果に組み合わせることができます。 クエリ結果に 2 つの異なる属性を選択すると、Configuration Manager は自動的にクエリの結合を作成しますが、[**結合**] タブには、より詳細なオプションが用意されています。 次の表は、System Center 2012 Configuration Manager がサポートする属性クラスを示しています。  

    |結合の種類|説明|  
    |---------------|-----------------|  
    |内部|一致する結果のみを表示します。自動的に作成される結合で常に使用されます。|  
    |左|基本属性についてはすべての結果を表示し、結合の属性については一致する結果だけを表示します。|  
    |権限|結合の属性についてはすべての結果を表示し、基本属性については一致する結果だけを表示します。|  
    |完全|基本属性と結合の属性の両方について、すべての結果を表示します。|  

     結合操作を使用する方法の詳細については、SQL Server のドキュメントを参照してください。  

10. **[OK]** を選択して *[&lt;クエリ名\>* **ステートメントのプロパティ]** ダイアログ ボックスを閉じます。  

11. **クエリの作成ウィザード**の **[全般]** タブで、クエリ結果を、コレクションのメンバーに制限しないか、指定したコレクションのメンバーに制限するか、クエリを実行するたびにコレクションの入力を求めるかを指定します。  

12. ウィザードを完了すると、クエリが作成されます。 新しいクエリが表示される、 **クエリ** 内のノード、 **監視** ワークスペース。  

##  <a name="BKMK_Import"></a> クエリをインポートする方法  
 Configuration Manager にクエリをインポートするには、この手順に従います。 クエリのエクスポート方法については、「[System Center Configuration Manager でクエリを管理する方法](../../../core/servers/manage/manage-queries.md)」を参照してください。  

#### クエリをインポートするには
<a id="to-import-a-query" class="xliff"></a>  

1.  Configuration Manager コンソールで、**[監視]** をクリックします。  

2.  **[監視]** ワークスペースで、**[クエリ]** を選択します。 **[ホーム]** タブの **[作成]** グループで、**[オブジェクトのインポート]** を選択します。  

3.  **オブジェクトのインポート ウィザード**の **[MOF ファイル名]** ページで、**[参照]** を選択して、インポートするクエリを含む管理オブジェクト フォーマット (MOF) ファイルを選択します。  

4.  インポートされるクエリの情報を確認して、ウィザードを完了します。 新しいクエリは、**[監視]** ワークスペースの **[クエリ]** ノードに表示されます。  

##  <a name="BKMK_Example"></a> Example WQL queries

このセクションでは、階層で使用したり、他の目的のために変更したりできる WMI クエリの例を示します。 これらのクエリを使用するには、**[クエリ ステートメントのプロパティ]** ダイアログ ボックスで **[クエリ言語を表示する]** を選択します。 次に、クエリをコピーして **[クエリ ステートメント]** フィールドに貼り付けます。  

> [!TIP]  
> 任意の文字列を表すには、ワイルドカード文字 `%` を使用します。 たとえば、`%Visio%` は、Microsoft Office Visio 2010 を返します。  

### Windows 7 を実行しているコンピューター
<a id="computers-that-run-windows-7" class="xliff"></a>

Windows 7 を実行しているすべてのコンピューターの NetBIOS 名とオペレーティング システムのバージョンを返すには、次のクエリを使用します。  

> [!TIP]  
> Windows Server 2008 R2 を実行しているコンピューターを返すには、`%Workstation 6.1%` を `%Server 6.1%` に変更します。  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### 特定のソフトウェア パッケージがインストールされているコンピューター
<a id="computers-with-a-specific-software-package-installed" class="xliff"></a>  

特定のソフトウェア パッケージがインストールされているすべてのコンピューターの NetBIOS 名とソフトウェア パッケージ名を返すには、次のクエリを使用します。 この例では、いずれかのバージョンの Microsoft Visio がインストールされているすべてのコンピューターが表示されます。 `%Visio%` を、クエリで照会するソフトウェア パッケージに置き換えます。  

> [!TIP]  
> このクエリは、Windows コントロール パネルのプログラムの一覧に表示される名前を使用して、ソフトウェア パッケージを検索します。  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### 特定の Active Directory ドメイン サービス組織単位にあるコンピューター
<a id="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit" class="xliff"></a>

指定した組織単位 (OU) 内のすべてのコンピューターの NetBIOS 名と OU 名を返すには、次のクエリを使用します。 テキスト `OU Name` を、クエリで照会する OU の名前に置き換えます。  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### 特定の NetBIOS 名のコンピューター
<a id="computers-with-a-specific-netbios-name" class="xliff"></a>

特定の文字列で始まるすべてのコンピューターの NetBIOS 名を返すには、次のクエリを使用します。 この例では、クエリは、`ABC` で始まる NetBIOS 名を持つすべてのコンピューターを返します。  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> 特定の種類のデバイス

デバイスの種類は、Configuration Manager データベースのリソース クラス **sms_r_system** および属性名 **AgentEdition** の下に格納されます。 指定したデバイスの種類のエージェント エディションと一致するデバイスのみを取得するには、次のクエリを使用します。  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

*&lt;デバイス ID\>* に対して次のいずれかの値を使用します。  

|デバイスの種類|AgentEdition の値|  
|-----------------|---------------------------|  
|Windows デスクトップまたはラップトップ コンピューター|0|  
|Windows ARM ベースのデバイス (Windows RT を実行)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac コンピューター|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel System-on-a-Chip|12|  
|Unix および Linux サーバー|13|  

 たとえば、クエリで Mac コンピューターのみを返すには、次のクエリを使用します。  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## 関連項目
<a id="see-also" class="xliff"></a>  
 [System Center Configuration Manager でのクエリの操作とメンテナンス](../../../core/servers/manage/operations-and-maintenance-for-queries.md)

