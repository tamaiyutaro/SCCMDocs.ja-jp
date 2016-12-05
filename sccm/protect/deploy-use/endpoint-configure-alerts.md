---
title: "Endpoint Protection アラートの構成 | System Center Configuration Manager"
description: "Microsoft System Center 2012 Configuration Manager で Endpoint Protection アラートを構成する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 38abfd1823972f8fea9966d74ae7c00a48baeb8b


---

#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager での Endpoint Protection 用のアラートの構成

*適用対象: System Center Configuration Manager (Current Branch)*

 Microsoft System Center Configuration Manager で Endpoint Protection アラートを構成して、階層内でのマルウェア感染など、特定のイベントが発生したときに管理ユーザーに通知することができます。 通知は、Configuration Manager コンソールの Endpoint Protection ダッシュボードで、**[監視]** ワークスペースの **[アラート]** ノードに表示されます。また、指定されたユーザーに電子メールで通知を送信することもできます。

 Configuration Manager で Endpoint Protection 用のアラートを構成するには、このトピックの次の手順と補足手順に従います。

> [!IMPORTANT]
>  Endpoint Protection のアラートを構成するコレクションの **[セキュリティ ポリシーの実施]** アクセス許可が必要です。

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager で Endpoint Protection 用のアラートを構成する手順

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス コレクション**] をクリックします。

3.  **[デバイス コレクション]** 一覧で、アラートを構成するコレクションを選んでから、 **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。

    > [!NOTE]
    >  ユーザーのコレクションに対してアラートを構成することはできません。

4.  Configuration Manager コンソールの **[監視]** ワークスペースで、このコレクションのマルウェア対策操作についての詳細を表示する場合は、[*<コレクション名\>***のプロパティ**] ダイアログ ボックスの **[アラート]** タブで、**[このコレクションを Endpoint Protection ダッシュボードに表示する]** を選びます。

    > [!NOTE]
    >  このオプションは、[すべてのシステム] コレクションには選択できません。 ****

5.  [*<コレクション名\>***のプロパティ**] ダイアログ ボックスの **[アラート]** タブで、**[追加]** をクリックします。

6.  **[コレクションの新しいアラートの追加]** ダイアログ ボックスの **[Generate an alert when these conditions apply]** (これらの条件を満たす場合にアラートを生成する) セクションで、特定の Endpoint Protection イベントが発生したときに Configuration Manager が生成するアラートを選択してから、**[OK]** をクリックします。

7.  **[アラート]** タブの **[条件]** 一覧で、Endpoint Protection の各アラートを選択してから、次の情報を指定します。

    -   **アラート名** - 既定の名前を受け入れるか、新しいアラート名を入力します。

    -   **アラートの重要度** - この一覧で、Configuration Manager コンソールに表示されるアラート レベルを選択します。

8.  選択したアラートに応じて、次の追加情報を指定します。

    -   **[マルウェア検出]** - このアラートは、監視するコレクション内のコンピューターでマルウェアが検出されると、生成されます。 **[マルウェア検出のしきい値]** で、このアラートが生成されるマルウェア検出のレベルを指定します。

        -   **[高 - すべて検出]** - Endpoint Protection クライアントが実行する操作に関係なく、指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されます。

        -   **[中 - 検出、操作を保留中]** - 指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されます。マルウェアは、手動で削除する必要があります。

        -   **[低 - 検出、操作中]** - 指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されますが、マルウェアはアクティブなままです。

    -   **[マルウェア大量感染]** - このアラートは、監視するコレクション内の、指定した割合のコンピューターで特定のマルウェアが検出されると、生成されます。

        -   **[マルウェアが検出されたコンピューターの割合]** - コレクション内で、マルウェアが検出されたコンピューターの割合が指定したパーセンテージを超えると、アラートが生成されます。 割合を指定する **1** を通じて **99**です。

            > [!NOTE]
            >  パーセンテージの値は、コレクション内のコンピューターの数に基づきますが、構成マネージャー クライアントがインストールされていないコンピューターは除外されます。 これには Endpoint Protection クライアントがまだインストールされていないコンピューターが含まれます。

    -   **[マルウェア連続検出]** - このアラートは、監視するコレクション内のコンピューターで、指定した時間数にわたって指定した回数を超えて特定のマルウェアが検出されると、生成されます。 次の情報を指定して、このアラートを構成します。

        -   **マルウェアが検出された回数を超える:** -指定した回数よりも詳細のコレクション内のコンピューターで同じマルウェアが検出されたときに、アラートが生成されます。 値を指定して **2** を通じて **32**です。

        -   **[検出期間 (時間):]** マルウェアの検出の数が行う必要があります (単位は時間) の検出間隔を指定します。 **[1]** から **[168]**までの数で指定します。

    -   **[複数のマルウェア検出]** - このアラートは、監視するコレクション内のコンピューターで、指定した時間数にわたって指定した種類の数を超えたマルウェアが検出されると、生成されます。 次の情報を指定して、このアラートを構成します。

        -   **[検出されたマルウェアの種類の数:]** 別のマルウェアの種類の指定した数が、コレクション内のコンピューターで検出されたときに、アラートが生成されます。 値を指定して **2** を通じて **32**です。

        -   **[検出期間 (時間):]** マルウェアの検出の数が発生する必要がありますを時間単位では、検出の間隔を指定します。 **[1]** から **[168]**までの数で指定します。

9. **[OK]** をクリックして [*<コレクション名\>***のプロパティ**] ダイアログ ボックスを閉じます。  

> [!div class="button"]
[次のステップ >](endpoint-definition-updates.md)

> [!div class="button"]
[戻る >](endpoint-protection-site-role.md)



<!--HONumber=Nov16_HO1-->

