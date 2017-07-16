---
title: "オンプレミス インフラストラクチャのアップグレード | Microsoft Docs"
description: "SQL Server やサイト システムのサイト オペレーティング システムなどのインフラストラクチャをアップグレードする方法について説明します。"
ms.custom: na
ms.date: 06/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0564cb678200d17d97c0f1d111c0b4b41d8ba40e
ms.openlocfilehash: 188b7f2537dd0e569a5c00995620124512cf311b
ms.contentlocale: ja-jp
ms.lasthandoff: 06/30/2017


---
# System Center Configuration Manager をサポートするオンプレミス インフラストラクチャのアップグレード
<a id="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を実行するサーバー インフラストラクチャをアップグレードする場合は、このトピックの情報を参考にしてください。  

 - 以前バージョンの Configuration Manager から System Center Configuration Manager にアップグレードする場合は、「[Upgrade to System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)」(System Center Configuration Manager へのアップグレード) を参照してください。

- System Center Configuration Manager インフラストラクチャを新しいバージョンにアップグレードする場合は、「[System Center Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」を参照してください。

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> サイト システムのサイト オペレーティング システムのアップグレード  
 Configuration Manager には、次の状況で、サイト サーバーをホストするサーバーとサイト システムの役割をホストするリモート サーバーのオペレーティング システムの一括アップグレードをサポートしています。  

-   アップグレード後の Service Pack レベルが Configuration Manager によってサポートされている場合の、Windows Server の上位 Service Pack への一括アップグレード。  
-   以下の一括アップグレード。
    - Windows Server 2012 R2 から Windows Server 2016 ([詳細を参照](#bkmk_2016))。
    - Windows Server 2012 から Windows Server 2016 ([詳細を参照](#bkmk_2016))。
    - Windows Server 2012 から Windows Server 2012 R2 ([詳細を参照](#bkmk_2012r2))。
    - Configuration Manager バージョン 1602 以降を使用する場合は、Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレードもサポート ([詳細を参照](#bkmk_from2008r2))。

    > [!WARNING]  
    >  Windows Server 2012 R2 にアップグレードする前に、サーバーから *WSUS 3.2 をアンインストールする必要があります* 。  
    >   
    >  この重要な手順の詳細については、Windows Server ドキュメントの「[Windows Server Update Services の概要](https://technet.microsoft.com/library/hh852345.aspx)」の「新機能と変更された機能」セクションを参照してください。  

サーバーをアップグレードするには、アップグレード先のオペレーティング システムによって提供されるアップグレード手順を使用します。  以下を参照してください。
  -  Windows Server のドキュメントの「[Windows Server 2012 R2 のアップグレード オプション](https://technet.microsoft.com/library/dn303416.aspx)」。  
  - Windows Server のドキュメントの「[Windows Server 2016 のアップグレード オプションと変換オプション](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths)」。

### <a name="bkmk_2016"></a> Windows Server 2012 または Windows Server 2012 R2 から Windows Server 2016 へのアップグレード
Windows Server 2012 または Windows Server 2012 R2 から Windows Server 2016 にアップグレードする場合は、以下が適用されます。


**アップグレード前:**  
-   System Center Endpoint Protection (SCEP) クライアントを削除します。 Windows Server 2016 では、SCEP クライアントの代わりとして、Windows Defender が組み込まれています。 SCEP クライアントが存在している場合、Windows Server 2016 へのアップグレードが妨げられる可能性があります。

**アップグレード後:**
-   Windows Defender が有効であり、自動開始が設定され、実行されていることを確認します。
-   次の Configuration Manager のサービスが実行されていることを確認します。
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
  -     サイト サーバー
  -     管理ポイント
  -     アプリケーション カタログ Web サービス ポイント
  -     アプリケーション カタログ Web サイト ポイント

-   サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

-   不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。

**リモートの Configuration Manager コンソールに関する既知の問題:**  
サイト サーバーまたは SMS_Provider のインスタンスをホストするサーバーを Windows Server 2016 にアップグレードした後、管理ユーザーが Configuration Manager コンソールをサイトに接続できない場合があります。 この問題を回避するには、WMI の SMS Admins グループのアクセス許可を手動で復元する必要があります。 サイト サーバーと、SMS_Provider のインスタンスをホストする各リモート サーバーで、アクセス許可を設定する必要があります。

1. 該当するサーバー上で Microsoft 管理コンソール (MMC) を開き、**WMI コントロール**のスナップインを追加し、**[ローカル コンピューター]** を選択します。
2. MMC で、**[WMI コントロール (ローカル)]** の **[プロパティ]** を開き、**[セキュリティ]** タブを選択します。
3. ルートの下のツリーを展開し、**[SMS]** ノードを選択して、**[セキュリティ]** を選択します。  **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。
  -     アカウントの有効化
  -     リモートの有効化
4. **[セキュリティ] タブ**で、**[SMS]** ノードの下にある **[site_&lt;sitecode**>] ノードを選択し、次に **[セキュリティ]** を選択します。 **SMS Admins** グループに次のアクセス許可が付与されていることを確認します。
  -   メソッドの実行
  -   プロバイダーによる書き込み
  -   アカウントの有効化
  -   リモートの有効化
5. アクセス許可を保存して、Configuration Manager コンソールへのアクセスを復元します。

### <a name="bkmk_2012r2"></a>Windows Server 2012 から Windows Server 2012 R2

**アップグレード前:**
-  他のサポートされるシナリオとは異なり、このシナリオではアップグレードの前に特別な考慮事項は必要ありません。

**アップグレード後:**
  - Windows 展開サービスが開始され、次のサイト システムの役割を実行していることを確認します (このサービスはアップグレード時に停止されます)。
    - サイト サーバー
    - 管理ポイント
    - アプリケーション カタログ Web サービス ポイント
    - アプリケーション カタログ Web サイト ポイント

  -     **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
    -   サイト サーバー
    -   管理ポイント
    -   アプリケーション カタログ Web サービス ポイント
    -   アプリケーション カタログ Web サイト ポイント


  -     サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

  不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。

### <a name="bkmk_from2008r2"></a>Windows Server 2008 R2 から Windows Server 2012 R2 へのアップグレード
このオペレーティング システムのアップグレード シナリオには、次のような条件があります。  

**アップグレード前:**
-   WSUS 3.2 をアンインストールします。  
    サーバー オペレーティングシステムを Windows Server 2012 R2 にアップグレードする前に、サーバーから WSUS 3.2 をアンインストールする必要があります。 この重要な手順の詳細については、Windows Server ドキュメントの「Windows Server Update Services の概要」の「新機能と変更された機能」セクションを参照してください。

**アップグレード後:**
  - Windows 展開サービスが開始され、次のサイト システムの役割を実行していることを確認します (このサービスはアップグレード時に停止されます)。
    - サイト サーバー
    - 管理ポイント
    - アプリケーション カタログ Web サービス ポイント
    - アプリケーション カタログ Web サイト ポイント


  -     **Windows プロセス アクティブ化**サービスと **WWW/W3svc** サービスが有効であり、自動開始が設定され、次のサイト システムの役割で実行されていることを確認します (これらのサービスはアップグレード時に無効になります)。
    -   サイト サーバー
    -   管理ポイント
    -   アプリケーション カタログ Web サービス ポイント
    -   アプリケーション カタログ Web サイト ポイント


  -     サイト システムの役割をホストする各サーバーが、そのサーバーで実行される[サイト システムの役割の前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)のすべてを引き続き満たしていることを確認します。 たとえば、BITS、WSUS を再インストールしたり、IIS の特定の設定を構成したりすることが必要になる場合があります。

  不足している前提条件を復元した後で、もう一度サーバーを再起動して、サービスが開始され、動作していることを確認します。


### サポートされていないアップグレードのシナリオ
<a id="unsupported-upgrade-scenarios" class="xliff"></a>
次の Windows Server のアップグレード シナリオは、よく問い合わせが寄せられますが、Configuration Manager ではサポートされていません。  

-   Windows Server 2008 から Windows Server 2012 以降  
-   Windows Server 2008 R2 から Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Configuration Manager クライアントのオペレーティング システムのアップグレード  
 次の状況で、Configuration Manager は Configuration Manager クライアントのオペレーティング システムの一括アップグレードをサポートします。  

-   アップグレード後の Service Pack レベルが Configuration Manager によってサポートされている場合の、Windows の上位 Service Pack への一括アップグレード。  

-   Windows のサポートされているバージョンから Windows 10 への一括アップグレード。 詳細については、「[System Center Configuration Manager を使用して、Windows を最新のバージョンにアップグレードする](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

-   Windows 10 のビルドからビルドへのサービス アップグレード。  詳細については、「[System Center Configuration Manager を使用して、サービスとしての Windows を管理する](../../../osd/deploy-use/manage-windows-as-a-service.md)」をご覧ください。  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> サイト データベース サーバーでの SQL Server のアップグレード  
  Configuration Manager では、サイト データベース サーバー上の SQL のサポートされたバージョンからの、SQL Server の一括アップグレードをサポートしています。 このセクションの SQL Server のアップグレード シナリオは Configuration Manager でサポートされており、各シナリオの要件を含んでいます。

 Configuration Manager によってサポートされている SQL Server のバージョンの詳細については、「[System Center Configuration Manager の SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)」を参照してください。  

 **SQL Server のサービス パック バージョンのアップグレード:**    
 Configuration Manager は、アップグレード後の SQL Server の Service Pack レベルが Configuration Manager によってサポートされている場合、SQL Server の上位 Service Pack への一括アップグレードをサポートします。

 1 つの階層に複数の Configuration Manager サイトがある場合は、各サイトで SQL Server の異なるサービス パックのバージョンを実行できます。また、サイトがサイト データベースに使用する SQL Server のサービス パックのバージョンをアップグレードする順序に制限はありません。

 **SQL Server の新しいバージョンへのアップグレード:**   
 Configuration Manager は次のバージョンへの SQL Server の一括アップグレードをサポートしています。

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

各サイトでサイト データベースをホストする SQL Server のバージョンをアップグレードする場合は、サイトで使用される SQL Server のバージョンを、次の順序でアップグレードする必要があります。

 1. 最初に中央管理サイトで SQL Server をアップグレードします。
 2. セカンダリ サイトの親プライマリ サイトをアップグレードする前に、セカンダリ サイトをアップグレードします。
 3. 最後に親プライマリ サイトをアップグレードします。 これには、中央管理サイトに報告する子プライマリ サイトと、階層の最上位サイトであるスタンドアロンのプライマリ サイトの両方が含まれます。

**SQL Server の基数推定レベルおよびサイト データベース:**   
サイト データベースを以前のバージョンの SQL Server からアップグレードすると、既存の SQL 基数推定 (CE) レベルが SQL Server のそのインスタンスで許可されている最小レベルである場合に、データベースではそのレベルが保持されます。 許可レベルより低い互換性レベルのデータベースを持つ SQL Server をアップグレードすると、データベースは SQL で許可されている最も低い互換性レベルに設定されます。

次の表に、Configuration Manager サイト データベースで推奨される互換性レベルを示します。

|SQL Server バージョン | サポートされる互換性レベル |推奨レベル|
|----------------|--------------------|--------|
| SQL Server 2016| 130、120、110、100 | 130|
| SQL Server 2014| 120、110、100      | 110|

サイト データベースで使用されている SQL Server の CE 互換性レベルを識別するには、サイト データベース サーバーで **SELECT name, compatibility_level FROM sys.databases** という SQL クエリを実行します。

 SQL CE の互換性レベルとその設定方法の詳細については、「[ALTER DATABASE 互換性レベル (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)」を参照してください。


SQL Server の詳細については、TechNet にある SQL Server のドキュメントを参照してください。
-   [SQL Server 2012 へのアップグレード](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [SQL Server 2014 へのアップグレード](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [SQL Server 2016 へのアップグレード](https://technet.microsoft.com/library/bb677622(v=sql.130))



### サイト データベース サーバー上の SQL Server をアップグレードするには
<a id="to-upgrade-sql-server-on-the-site-database-server" class="xliff"></a>  

1.  サイトのすべての Configuration Manager サービスを停止します。  
2.  SQL Server をサポートされるバージョンにアップグレードします。  
3.  Configuration Manager サービスを再起動します。  

> [!NOTE]  
>  中央管理サイトで使用している SQL Server のエディションを Standard エディションから Datacenter エディションまたは Enterprise エディションに変更する際には、階層がサポートするクライアントの数を制限するデータベースのパーティションは変更しません。

