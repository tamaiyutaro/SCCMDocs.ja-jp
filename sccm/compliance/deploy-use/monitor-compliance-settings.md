---
title: "コンプライアンス設定を監視する | Microsoft Docs"
description: "構成基準のコンプライアンスのステータスを表示するには、このトピックの 1 つ以上の手順を使用します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 75cd7e811262633d81d978265f21ec7ed3b61a58


---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>System Center Configuration Manager でコンプライアンス設定を監視する

*適用対象: System Center Configuration Manager (Current Branch)*

階層のデバイスに System Center Configuration Manager 構成基準を展開した後は、このトピックの 1 つ以上の手順を使用して、構成基準のコンプライアンス ステータスを表示することができます。

> [!NOTE]  
>  コンプライアンス設定レポートの評価基準フィールド (クライアント側のレポートでは [制約] ****) に、基盤となるサービス モデリング言語 (SML) が表示されます。 これは、Configuration Manager コンソールに構成アイテムを作成した管理者が SML に精通していない場合、検証条件を把握するのを妨げる可能性があります。 この場合は、Configuration Manager コンソールの **[監視]** ワークスペースを使用して、構成アイテムおよび評価基準のプロパティを表示します。  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager コンソールでのコンプライアンス結果の表示  
 Configuration Manager コンソールで、展開した構成基準のコンプライアンスの詳細を表示するには、この手順に従います。  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager コンソールでのコンプライアンス結果の表示  

1.  Configuration Manager コンソールで、**[監視]** > **[展開]** の順にクリックします。  

3.  [展開] **** の一覧で、コンプライアンス情報を表示する構成基準の展開を選択します。  

4.  メイン ページでは、構成基準の展開のコンプライアンスについて概要を確認することができます。 詳細を表示するには構成基準の展開を選択し、[ホーム] **** タブの [展開] **** グループで、[ステータスの表示] **** をクリックして [展開のステータス] **** ページを開きます。  

     [展開のステータス] **** ページには次のタブがあります。  

    -   **対応**: 影響を受けた資産の数に基づいて、構成基準のコンプライアンスを表示します。 ルールをクリックして、そのルールに準拠するすべてのユーザーとデバイスを含む [資産とコンプライアンス] **** ワークスペースの[ユーザー] **** または [デバイス] **** のノードの下に一時ノードを作成できます。 [資産の詳細] **** ウィンドウはその構成基準に準拠するユーザーやデバイスを表示します。 一覧のユーザーまたはデバイスをダブルクリックすると、追加の情報が表示されます。  

        > [!IMPORTANT]  
        >  クライアント デバイスで検知されていない、または該当しない構成アイテム ルールは評価されませんが、ルールは対応という結果を戻します。  

    -   **エラー**: 影響を受けた資産の数に基づいて、選択した構成基準の展開におけるすべてのエラーの一覧を表示します。 ルールをクリックして、そのルールでエラーとなったすべてのユーザーとデバイスを含む [資産とコンプライアンス] **** ワークスペースの [ユーザー] **** または [デバイス] **** のノードの下に一時ノードを作成できます。 ユーザーまたはデバイスを選択すると、[資産の詳細] **** ウィンドウは選択された問題に影響を受けているユーザーやデバイスを表示します。 一覧のユーザーまたはデバイスをダブルクリックすると、問題につていの追加の情報が表示されます。  

    -   **非対応**: 影響を受けた資産の数に基づいて、その構成基準内のすべてのコンプライアンス非対応のルールの一覧を表示します。 ルールをクリックして、そのルールのコンプライアンスに非対応となったすべてのユーザーとデバイスを含む [資産とコンプライアンス] **** ワークスペースの [ユーザー] **** または [デバイス] **** のノードの下に一時ノードを作成できます。 ユーザーまたはデバイスを選択すると、[資産の詳細] **** ウィンドウは選択された問題に影響を受けているユーザーやデバイスを表示します。 一覧のユーザーまたはデバイスをダブルクリックすると、問題について追加の情報が表示されます。  

    -   **不明**: 選択した構成基準の展開に対するコンプライアンスが報告されなかったすべてのユーザーとデバイスの一覧が、現在のデバイスのクライアント ステータスと共に表示されます。  

5.  [展開のステータス] **** ページで、展開された構成基準のコンプライアンスについての詳細を確認できます。 [展開] **** ノードの下に一時ノードが作成されるため、後から再度この情報をすばやく確認できます。  

##  <a name="view-compliance-results-by-using-reports"></a>レポートを使用してコンプライアンス結果を表示する  
 Configuration Manager のコンプライアンス設定には、無数の組み込みレポートが含まれており、構成アイテム、構成基準、および展開についての情報監視に便利です。 これらのレポートには、[コンプライアンスおよび設定管理] ****のカテゴリがあります。  

> [!IMPORTANT]  
>  コンプライアンス設定でレポートの**%**[デバイス フィルター] **と [ユーザー フィルター] パラメーターを指定するときは必ず、ワイルドカード (** ) 文字を使ってください。  

 Configuration Manager でのレポートの構成方法に関して詳しくは、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Configuration Manager の Windows クライアント コンピューターでコンプライアンス結果を表示する

> [!NOTE]  
>  ドメインのゲスト アカウントでログオンしている場合、Configuration Manager Windows クライアントの情報は表示できません。    

1.  クライアント コンピューターのコントロール パネルで [Configuration Manager] **** に移動し、ダブルクリックしてプロパティを開きます。  

2.  [構成] **** タブをクリックし、展開された構成基準の一覧を表示します。  

3.  各構成基準の [コンプライアンス対応状態] **** を表示します。  

    > [!IMPORTANT]  
    >  評価結果は、クライアントに 15 分間キャッシュされます。 15 分以内に再評価を開始すると、新たに評価した結果ではなく、このキャッシュのコンプライアンス結果が返されます。 このため、クライアントで対応評価の結果に影響する変更を行った場合は、15 分以上待ってから再評価を開始してください。  

    -   **対応**: クライアント コンピューターは、評価された構成基準に対応しています。  

    -   **非対応**: クライアント コンピューターは、評価された構成基準に対応していません。  

    -   **不明**: クライアント コンピューターは構成基準をまだ評価していません。 対応評価スケジュールとは別に評価を開始する場合は、評価する構成基準を選択し、[評価] ****をクリックします。  

        > [!NOTE]  
        >  クライアント コンピューターにローカルな管理者資格がある場合は、評価された各構成基準の詳細を表示し、どの構成項目がコンプライアンス非対応状態かを判別できます。 これを行うには、構成基準を選択して、 **[レポートの表示]**をクリックします。  

4.  **[OK]**をクリックします。  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>構成基準のコンプライアンスに基づいてコレクションを作成する  
 指定したコンプライアンスのデバイスに基づいて、Configuration Manager コレクションを作成するには次の手順に従います。 次のコンプライアンス状態に基づいて、コレクションを作成することができます。  

-   **対応**  

-   **エラー**  

-   **Non-compliant**  

-   **不明**  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成基準]** の順にクリックします。  

3.  [構成基準] **** の一覧で、コレクションを作成する構成基準を選択します。  

4.  [展開] **** タブの [展開] ****グループで、[新しいコレクションの作成] **** をクリックし、ドロップダウン リストから作成するコレクションに適用するコンプライアンスのレベルを選択します。  

5.  構成項目の展開がユーザーか、デバイスかによって、ユーザー コレクションの作成ウィザード **** またはデバイス コレクションの作成ウィザード **** が開きます。 ウィザードは自動的にコレクションを作成するための正しい値を挿入しますが、これらの値は編集することができます。  

6.  ウィザードを完了すると、[資産とコンプライアンス] **** ワークスペースの [ユーザー コレクション] **** または [デバイス コレクション] **** ノードにコレクションが表示されます。  



<!--HONumber=Dec16_HO3-->


