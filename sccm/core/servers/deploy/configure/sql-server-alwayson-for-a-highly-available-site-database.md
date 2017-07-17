---
title: SQL Server Always On | Microsoft Docs
description: "SCCM での SQL Server Always On 可用性グループの使用を計画します。"
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 188ae877368a6cb2ec9998bff74259b4e5b5e7ce
ms.contentlocale: ja-jp
ms.lasthandoff: 06/01/2017


---
# Configuration Manager で SQL Server Always On 可用性グループを使用するための準備
<a id="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で、サイト データベース用の高可用性と障害復旧ソリューションとして SQL Server Always On 可用性グループを使用するための準備を行います。  
Configuration Manager では、次の場所での可用性グループの使用がサポートされます。
-     プライマリ サイトと中央管理サイト。
-     オンプレミス、または Microsoft Azure。

Microsoft Azure で可用性グループを使用する場合は、*Azure 可用性セット*を使用することで、サイト データベースの可用性をさらに向上できます。 Azure 可用性セットの詳細については、「 [仮想マシンの可用性管理](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/)」を参照してください。

>  [!Important]   
>  作業を続行する前に、SQL Server と SQL Server 可用性グループの構成に慣れておいてください。 以下の情報では、SQL Server ドキュメント ライブラリと手順を示します。

## サポートされるシナリオ
<a id="supported-scenarios" class="xliff"></a>
Configuration Manager で可用性グループを使用する場合にサポートされるシナリオを以下に示します。 それぞれの詳細と手順については、[Configuration Manager の可用性グループの構成](/sccm/core/servers/deploy/configure/configure-aoag)に関するページを参照してください。


-      [Configuration Manager で使用する可用性グループを作成します](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)。
-     [可用性グループを使用するようにサイトを構成します](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)。
-     [サイト データベースをホストする可用性グループでレプリカ メンバーを追加または削除します](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-replica-members)。
-     [サイト データベースを、可用性グループから、スタンドアロン SQL Server の指定したインスタンスまたは既定のインスタンスに移動します](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)。


## 必要条件
<a id="prerequisites" class="xliff"></a>
すべてのシナリオに以下の必要条件が適用されます。 追加の必要条件が特定のシナリオに適用される場合は、そのシナリオで詳しく説明します。   

### Configuration Manager のアカウントとアクセス許可
<a id="configuration-manager-accounts-and-permissions" class="xliff"></a>
**サイト サーバーからレプリカ メンバーへのアクセス:**   
サイト サーバーのコンピューター アカウントは、可用性グループのメンバーである各コンピューターの **ローカル管理者** グループのメンバーである必要があります。

### SQL Server
<a id="sql-server" class="xliff"></a>
**バージョン:**  
可用性グループの各レプリカは、使用しているバージョンの Configuration Manager でサポートされるバージョンの SQL Server を実行する必要があります。 SQL Server でサポートされる場合、可用性グループの別々のノードで、異なるバージョンの SQL Server を実行できます。

**エディション:**  
SQL Server の *Enterprise* エディションを使用する必要があります。

**アカウント:**  
SQL Server の各インスタンスは、ドメイン ユーザー アカウント (**サービス アカウント**) または**ローカル システム**で実行できます。 グループ内の各レプリカは別の構成を持つことができます。 [SQL Server のベスト プラクティス](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd)に従って、使用可能な最小アクセス許可を持つアカウントを使用します。

たとえば、SQL Server 2016 用にサービス アカウントとアクセス許可を構成する場合は、MSDN の「[Configure Windows Service Accounts and Permissions](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions)」 (Windows サービス アカウントとアクセス許可の構成) を参照してください。

  **ローカル システム**を使用してレプリカを実行する場合は、エンドポイント認証を構成する必要があります。 これには、レプリカ サーバー エンドポイントへの接続を有効にする権限の委任が含まれます。
  -     SQL Server の権限を委任するには、ノードの他の SQL Server にログイン情報として各 SQL Server のコンピューター アカウントを追加し、そのアカウントに SA 権限を付与します。  
  -     各レプリカで以下のスクリプトを実行し、ローカル エンドポイントの各リモート サーバーにエンドポイント権限を委任します。    

              GRANT CONNECT ON endpoint::[endpoint_name]  
              TO [domain\servername$]

詳細については、[Always On 可用性グループのデータベース ミラーリング エンドポイントの作成](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell)に関するページを参照してください。

### 可用性グループの構成
<a id="availability-group-configurations" class="xliff"></a>
**レプリカ メンバー:**  
可用性グループには、1 つのプライマリ レプリカを含める必要があり、最大 2 つの同期セカンダリ レプリカを含めることができます。  各レプリカ メンバーには以下が必要です。
-   **既定のインスタンス**を使用する  
    *バージョン 1702 以降では、****名前付きインスタンス***を使用できます。

-      **[プライマリ ロールでの接続]** が **[はい]** に設定されている
-      **[読み取り可能なセカンダリ]** が **[はい]** に設定されている  
-      **手動フェールオーバー**に設定されている       

    >  [!TIP]
    >  Configuration Manager では、**[自動フェールオーバー]** に設定されている場合、可用性グループ レプリカの使用がサポートされます。 ただし、次のような場合は **[手動フェールオーバー]** を設定する必要があります。
    >  -  セットアップを実行して、可用性グループでのサイト データベースの使用を指定する。
    >  -  Configuration Manager に (サイト データベースに適用される更新プログラムだけでなく) すべての更新プログラムをインストールする場合。  

**レプリカ メンバーの場所:**  
可用性グループ内のすべてのレプリカはオンプレミスまたは Microsoft Azure でホストする必要があります。 オンプレミス メンバーと Azure のメンバーを含むグループはサポートされていません。     

Azure で可用性グループをセットアップし、グループが内部または外部ロード バランサーの背後にある場合に、セットアップで各レプリカにアクセスできるようにするために開く必要がある既定ポートは以下のとおりです。   

-      RCP エンドポイント マッパー - **TCP 135**   
-      サーバー メッセージ ブロック – **TCP 445**  
    *データベースの移動が完了した後で、このポートを削除することができます。バージョン 1702 以降では、このポートは必要なくなりました。*
-      SQL Server Service Broker - **TCP 4022**
-      SQL over TCP – **TCP 1433**   

セットアップの完了後に、次のポートが引き続きアクセス可能である必要があります。
-      SQL Server Service Broker - **TCP 4022**
-      SQL over TCP – **TCP 1433**

バージョン 1702 以降では、これらの構成でカスタム ポートを使用することができます。 エンドポイントと、可用性グループ内のすべてのレプリカで、同じポートを使用する必要があります。


**リスナー:**   
可用性グループには、少なくとも 1 つの **可用性グループ リスナー**が必要です。 可用性グループのサイト データベースを使用するよう Configuration Manager を構成するときには、このリスナーの仮想名が使用されます。 可用性グループに複数のリスナーを含めることはできますが、Configuration Manager で使用できるのは 1 つだけです。 詳細については、「[Create or Configure an Availability Group Listener (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server)」 (可用性グループ リスナーの作成または構成 (SQL Server)) を参照してください。

**ファイル パス:**   
可用性グループ内のデータベースを使用するようにサイトを構成するために Configuration Manager のセットアップを実行するときには、各セカンダリ レプリカ サーバーに、現在のプライマリ レプリカで検出されたサイト データベース ファイルのファイル パスと同じ SQL Server ファイル パスが存在する必要があります。
-   同じパスが存在しない場合、セットアップでは、サイト データベースの新しい場所として可用性グループのインスタンスを追加できません。
-   さらに、ローカル SQL Server サービス アカウントは、このフォルダーに対する**フル コントロール** アクセス許可を持っている必要があります。

セットアップで可用性グループのデータベース インスタンスを指定するときに、セカンダリ レプリカ サーバーにはこのファイルのパスのみが必要です。 セットアップで可用性グループのサイト データベースの構成が完了したら、セカンダリ レプリカ サーバーから未使用のパスを削除できます。

たとえば、次の場合を考えてください。
-    3 つの SQL Server を使用する可用性グループを作成するとします。

-    プライマリ レプリカ サーバーは、SQL Server 2014 の新規インストールです。 既定では、データベースの .MDF および .LDF ファイルが C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA に格納されます。

-    両方のセカンダリ レプリカ サーバーが前のバージョンから SQL Server 2014 にアップグレードされており、データベース ファイルを格納する元のファイル パス (つまり、C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA) を保持します。

-    この可用性グループへのサイト データベースの移動を試行する前に、各セカンダリ レプリカ サーバー上で C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA というファイル パス (プライマリ レプリカで使用されるのと同じパス) を作成する必要があります。セカンダリ レプリカでこのファイルの場所を使用しない場合でも必要です。

-    次に、各セカンダリ レプリカ上の SQL Server サービス アカウントに、そのサーバーの新規作成されたファイルの場所に対するフル コントロール アクセス許可を付与します。

-    この時点で Configuration Manager のセットアップを正常に実行して、可用性グループ内のサイト データベースを使用するようにサイトを構成できます。

**新しいレプリカでデータベースを構成する:**   
 各レプリカのデータベースは、次のように設定する必要があります。
-     **CLR 統合**を*有効*にする必要があります。
-      **max text repl size** を *2147483647* にする必要があります。
-      データベース所有者を *SA アカウント*にする必要があります。
-      **TRUSTWORTY** を **ON** にする必要があります。
-      **Service Broker** を*有効*にする必要があります。

ライマリ レプリカでのみ、これらの構成を行うことができます。 セカンダリ レプリカを構成するには、まず、プライマリをセカンダリにフェールオーバーし、セカンダリを新しいプライマリ レプリカにする必要があります。   

必要に応じて SQL Server ドキュメントを使用すれば、設定の構成に役立ちます。 SQL Server ドキュメントの [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) や [CLR 統合](/sql/relational-databases/clr-integration/clr-integration-enabling)に関するページなどを参照してください。

### 検証スクリプト
<a id="verification-script" class="xliff"></a>
プライマリとセカンダリの両方のレプリカのデータベース構成を検証するために次のスクリプトを実行することができます。 セカンダリ レプリカに関する問題を修正するには、そのセカンダリ レプリカをプライマリ レプリカに変える必要があります。

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## 制限事項と既知の問題
<a id="limitations-and-known-issues" class="xliff"></a>
すべてのシナリオに以下の制限事項が適用されます。   

**基本的な可用性グループはサポートされない:**  
SQL Server 2016 Standard エディションで導入された[基本的な可用性グループ](https://msdn.microsoft.com/library/mt614935.aspx)では、Configuration Manager で使用するための要件であるセカンダリ レプリカに対する読み取りアクセスはサポートされていません。

**追加の可用性グループをホストする SQL Server:**   
SQL Server の可用性グループで 1 つ以上の可用性グループと、Configuration Manager で使用するグループをホストしている場合、Configuration Manager バージョン 1610 の前に、Configuration Manager セットアップの実行または Configuration Manager 用の更新プログラムをインストールするときに、これらの追加の各可用性グループの各レプリカに次の構成を設定する必要があります。
-   **手動フェールオーバー**
-     **読み取り専用接続を許可**

**サポートされていないデータベースの使用:**
-   **Configuration Manager は可用性グループ内のサイト データベースのみをサポートする:** 以下はサポートされていません。
    -   レポート データベース
    -   WSUS データベース
-   **既存のデータベース:** レプリカで作成された新しいデータベースを使用することはできません。 代わりに、可用性グループの構成時に、既存の Configuration Manager データベースのコピーをプライマリ レプリカに復元する必要があります。

**ConfigMgrSetup.log のセットアップ エラー:**  
セットアップを実行してサイト データベースを可用性グループに移動する場合、可用性グループのセカンダリ レプリカでデータベースの役割の処理が試行され、以下のようなエラーがログに記録されます。
-   エラー: SQL Server エラー: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]データベースが読み取り専用であるため、データベース "CM_AAA" をアップデートできませんでした。 Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

このようなエラーは無視してもかまいません。

## サイト バックアップの変更
<a id="changes-for-site-backup" class="xliff"></a>
**データベース ファイルのバックアップ:**  
可用性グループでサイト データベースを実行する場合は、一般的な Configuration Manager 設定とファイルをバックアップするために組み込み**バックアップ サイト サーバー** メンテナンス タスクを実行する必要があります。 ただし、そのバックアップで作成された .MDF ファイルや .LDF ファイルは使用しないでください。 代わりに、SQL Server を使用して、これらのデータベース ファイルの直接バックアップを作成します。

**トランザクション ログ:**  
サイト データベースの復旧モデルは、**[完全]** に設定する必要があります (可用性グループで使用する場合の要件)。 この構成で、サイト データベース トランザクション ログのサイズを監視および維持するための計画を立てます。 完全復旧モデルでは、データベースまたはトランザクション ログの完全バックアップが作成されるまで、トランザクションは書き込まれません。 詳細については、SQL Server のドキュメントの「[SQL Server データベースのバックアップと復元](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)」を参照してください。

## サイトの回復の変更
<a id="changes-for-site-recovery" class="xliff"></a>
可用性グループの 1 つ以上のノードがまだ機能している場合は、サイトの回復オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]** を使用できます。

 サイトを回復する前に、可用性グループのすべてのノードが失われた場合は、可用性グループを再作成する必要があります。 Configuration Manager では可用性ノードの再構築や復元はできません。 グループが再作成されて、バックアップが復元および再構成されたら、サイトの回復オプション **[データベースの回復をスキップする (このオプションは、サイト データベースが障害の影響を受けていない場合に選択してください)]** を使用できます。

詳細については、「[Backup and recovery for System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery)」 (System Center Configuration Manager のバックアップと回復) をご覧ください。

## レポートの変更
<a id="changes-for-reporting" class="xliff"></a>
**レポート サービス ポイントをインストールする:**  
レポート サービス ポイントでは、可用性グループのリスナーの仮想名の使用や SQL Server Always On 可用性グループ内のレポート サービス データベースのホスティングはサポートされていません。
-   既定では、レポート サービス ポイントのインストールで **[サイト データベース サーバー名]** がリスナーとして指定されている仮想名に設定されます。 これを変更し、可用性グループ内のレプリカのコンピューター名とインスタンスを指定します。
-   レポート作成の負荷を軽減する場合や、レプリカ ノードがオフラインのときに可用性を向上させる場合は、各レプリカ ノードで追加のレポート サービス ポイントをインストールすることと、独自のコンピューター名を指すように各レポート サービス ポイントを構成することを検討してください。

可用性グループの各レプリカでレポート サービス ポイントをインストールする場合、レポート作成時にアクティブなレポート ポイント サーバーにいつでも接続できます。

**コンソールで使用されるレポート サービス ポイントを切り替える:**  
レポートを実行するには、コンソールで **[監視]** > **[概要]** > **[レポートの作成]** > **[レポート]** の順に移動してから、**[レポート オプション]** を選択します。 [レポート オプション] ダイアログ ボックスで、目的のレポート サービス ポイントを選択します。

## 次のステップ
<a id="next-steps" class="xliff"></a>
必要条件、制限事項、および可用性グループを使用する場合に必要な一般的なタスクに関する変更を理解したら、「[Configure availability groups for Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag)」 (Configuration Manager の可用性グループの構成) を参照して、可用性グループを使用するためのサイトのセットアップおよび構成手順を確認してください。

