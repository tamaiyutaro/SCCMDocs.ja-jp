---
title: "System Center Configuration Manager へのアップグレード| Microsoft Docs"
description: "System Center 2012 Configuration Manager を実行しているサイトおよび階層から適切に一括アップグレードを実行するための手順を説明します。"
ms.custom: na
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 1166b739e1e8d667172d97883f484fdbc3a142c1
ms.contentlocale: ja-jp
ms.lasthandoff: 06/13/2017


---
# System Center Configuration Manager へのアップグレード
<a id="upgrade-to-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center 2012 Configuration Manager を実行しているサイトおよび階層から System Center Configuration Manager にアップグレードする、一括アップグレードを実行できます。  

 System Center 2012 Configuration Manager からアップグレードする前に、正常なアップグレードを妨げる可能性のある特定の構成を該当するサイトから削除し、複数のサイトが関係している場合は、特定のアップグレード順序に従う必要があります。  

 > [!TIP]
 > System Center Configuration Manager のサイトと階層のインフラストラクチャの管理において、*アップグレード*、*更新*、および*インストール* という用語は 3 つの異なる概念を説明するものです。 各用語の使用方法については、「[サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて](/sccm/core/understand/upgrade-update-install)」を参照してください。

##  <a name="bkmk_path"></a> 一括アップグレード パス  

**バージョン 1702 へのアップグレード**   
バージョン 1702 基準メディアがある場合は、次のバージョンを System Center Configuration Manager バージョン 1702 の正規ライセンス版にアップグレードできます。   
-     System Center Configuration Manager バージョン 1702 の評価版のインストール
-     System Center 2012 Configuration Manager Service Pack 1
-     System Center 2012 Configuration Manager Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager Service Pack 1

**バージョン 1606 へのアップグレード**  
2016 年 12 月 15 日に、バージョン 1606 の基準メディアが再リリースされ、追加のアップグレード シナリオのサポートが追加されました。 この新しいリリースでは、次のバージョンを System Center Configuration Manager バージョン 1606 の正規ライセンス版にアップグレードできます。  
-   System Center Configuration Manager バージョン 1606 の評価版
-   System Center Configuration Manager のリリース候補版のインストール  
-   System Center 2012 Configuration Manager Service Pack 1  
-   System Center 2012 Configuration Manager Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager Service Pack 1  

2016 年 12 月 15 日より前にダウンロードしたバージョン 1606 基準メディアを使用する場合は、System Center Configuration Manager バージョン 1606 の正規ライセンス版にアップグレードできるのは次のバージョンのみです。
-   System Center Configuration Manager バージョン 1606 の評価版
-   System Center 2012 Configuration Manager Service Pack 2
-   System Center 2012 R2 Configuration Manager Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  System Center 2012 Configuration Manager のバージョンから Current Branch にアップグレードするときには、アップグレード プロセスを効率化できることがあります。 詳細については、次をご覧ください。  
>   
>  -   [System Center Configuration Manager の更新プログラム](../../../../core/servers/manage/updates.md)の「[基準バージョンと更新プログラムのバージョン](../../../../core/servers/manage/updates.md#bkmk_Baselines)」セクション  
>  -   [System Center Configuration Manager の CD.Latest フォルダー](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **次はサポートされていません。**  
-   System Center Configuration Manager の Technical Preview から正規ライセンス版インストールへのアップグレードはサポートされていません。  Technical Preview バージョンは Technical Preview の新しいバージョンにのみアップグレードできます。  

-   Technical Preview から正規ライセンス版への移行はサポートされていません。  

##  <a name="bkmk_checklist"></a> アップグレードのチェックリスト  
 次のチェック リストは、System Center Configuration Manager への適切なアップグレードの計画に役立ちます。  

### アップグレードする前に
<a id="before-you-upgrade" class="xliff"></a>  

**System Center 2012 Configuration Manager 環境を確認し**、問題を解決する (詳細は KB4018655 にあり): [Configuration Manager クライアントが繰り返し発生する再試行タスクに起因して 5 時間おきに再インストールし、不注意なクライアント アップグレードを引き起こす可能性があります](https://support.microsoft.com/help/4018655)。

System Center Configuration Manager へのアップグレードに必要な**サポート対象構成をコンピューター環境が満たしていることを確認する**:  

サイト システムの役割をホストするために使うサーバー オペレーティング システムについて確認します。  

-   System Center 2012 Configuration Manager でサポートされている一部の古いオペレーティング システムは System Center Configuration Manager でサポートされていないため、アップグレードする前に、これらのオペレーティング システム上のサイト システムの役割を再配置するか削除する必要があります。 「[サイト システム サーバーでサポートされるオペレーティング システム](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)」の文書を参照してください。   
-   Configuration Manager の前提条件チェッカーでは、サイト サーバーやリモート サイト システムでのサイト システムの役割の前提条件は検証されません。  

サイト システムの役割をホストする各コンピューターについて、必要な前提条件を確認します。  

-   たとえば、System Center Configuration Manager では、オペレーティング システムを展開するために Windows 10 アセスメント & デプロイメント キット (Windows ADK) を使います。 セットアップを実行する前に、サイト サーバーと、SMS プロバイダーのインスタンスを実行する各コンピューターに Windows 10 ADK をダウンロードしてインストールする必要があります。  

サポートされているプラットフォームおよび前提条件の構成の全般的な情報については、「 [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

Configuration Manager と一緒に Windows ADK を使用する方法の詳細については、「[System Center Configuration Manager のオペレーティング システムの展開のインフラストラクチャ要件](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)」を参照してください。  

**サイトと階層の状態を確認して、未解決の問題がないことを確認する:**  
サイトをアップグレードする前に、サイト サーバー、サイト データベース サーバー、およびリモート コンピューターにインストールされているサイト システムの役割で、運用上のすべての問題を解決します。 運用上の問題があると、サイトのアップグレードが失敗する可能性があります。  

**サイト、サイト データベース サーバー、リモートのサイト システムの役割をホストするコンピューターのオペレーティング システムに適用できる、重要な更新プログラムすべてをインストールする:**  
サイトをアップグレードする前に、該当する各サイト システムの重要な更新プログラムすべてをインストールします。 更新のインストール時に再起動が必要な場合は、サービス パックの更新を開始する前に該当するコンピューターを再起動します。  

詳細については、「 [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851)」を参照してください。  

**System Center Configuration Manager でサポートされていないサイト システムの役割をアンインストールする:**  
次のサイト システムの役割は、System Center Configuration Manager では使用されなくなったため、System Center 2012 Configuration Manager からアップグレードする前にアンインストールする必要があります。  

-   帯域外管理ポイント  
-   システム正常性検証ツール ポイント  

**プライマリ サイトの管理ポイントのデータベース レプリカを無効にする:**  
Configuration Manager では、管理ポイントのデータベース レプリカが有効になっているプライマリ サイトを正常にアップグレードすることはできません。 次の操作を行う前に、データベースのレプリケーションを無効にしてください。  

-   データベースのアップグレードをテストするためにサイト データベースのバックアップを作成する  
-   実稼働サイトを System Center Configuration Manager にアップグレードする  

詳細については、次をご覧ください。  
-   System Center 2012 Configuration Manager: 「[管理ポイントのデータベース レプリカの構成](https://technet.microsoft.com/library/hh846234.aspx)」  
-   System Center Configuration Manager: 「[Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」 (System Center Configuration Manager の管理ポイントのデータベース レプリカ)  

**NLB を使用するソフトウェアの更新ポイントを再構成する:**  
Configuration Manager では、ネットワーク負荷分散 (NLB) クラスターを使用してソフトウェアの更新ポイントをホストしているサイトは、アップグレードできません。  

ソフトウェアの更新ポイントに NLB クラスターを使用している場合、PowerShell を使用して NLB クラスターを削除してください (System Center 2012 Configuration Manager SP1 以降、Configuration Manager に NLB クラスターを構成するためのオプションはありません)。  

**サイトのアップグレード時に各サイトですべてのサイト メンテナンス タスクを無効にする:**  
System Center Configuration Manager にアップグレードする前に、アップグレード プロセスがアクティブになっている間にそのサイトで実行される可能性があるサイトのメンテナンス タスクをすべて無効にします。 次のタスクが含まれますが、これらのタスクに限定されません。  

-   サイト サーバーのバックアップ  
-   期限切れのクライアント操作を削除  
-   期限切れの探索データの削除  

アップグレード プロセス中にサイト データベースのメンテナンス タスクが実行されると、サイトのアップグレードが失敗する可能性があります。  

タスクを無効にする前に、サイトのアップグレードが完了した後で構成を復元できるように、タスクのスケジュールを記録してください。  

サイトのメンテナンス タスクについて詳しくは、次をご覧ください。  

-   System Center 2012 Configuration Manager: 「[Configuration Manager のメンテナンス タスクの計画](https://technet.microsoft.com/library/gg712686.aspx)」  
-   System Center Configuration Manager: 「[System Center Configuration Manager のメンテナンス タスクのリファレンス](../../../../core/servers/manage/reference-for-maintenance-tasks.md)」  

**セットアップ前提条件チェッカーを実行する**:  
サイトをアップグレードする前に、セットアップとは別に **前提条件チェッカー** を実行して、サイトが前提条件を満たしていることを検証できます。 後でサイトをアップグレードしたときに、前提条件チェッカーが再度実行されます。  

2016 年 10 月リリースのバージョン 1606 の基準メディアを使用する場合、個別の前提条件チェックにより、System Center Configuration Manager の Current Branch と Long-Term Servicing Branch (LTSB) の両方にアップグレードするためにサイトが評価されます。 LTSB でサポートされていない機能がいくつかあるため、次のようなエントリが *ConfigMgrPrereq.log* に表示される場合があります。
 - 情報: サイトが LTSB エディションではありません。
 - LTSB エディションでサポートされていないサイト システムの役割 '資産インテリジェンス同期ポイント';    エラー;    Configuration Manager は '資産インテリジェンス同期ポイント' がインストールされていることを検出しました。 資産インテリジェンスは LTSB エディションでサポートされていません。 続行する前に、資産インテリジェンス同期ポイント サイト システムの役割をアンインストールする必要があります。

Current Branch にアップグレードする予定の場合は、LTSB エディションに関するエラーは無視してかまいません。 これらは、LTSB にアップグレードする予定の場合にのみ当てはまります。

後で Configuration Manager のセットアップを実行してアップグレードを行うときに、前提条件チェックが再度実行され、インストール対象として選択した System Center Configuration Manager のブランチに基づいてサイトが評価されます。 Current Branch にアップグレードする場合は、LTSB でサポートされていない機能のチェックは実行されません。

詳細については、「[System Center Configuration Manager の前提条件チェッカー](/sccm/core/servers/deploy/install/prerequisite-checker)」および「[System Center Configuration Manager の前提条件の確認の一覧](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)」を参照してください。  

**System Center Configuration Manager の前提条件ファイルと再頒布可能ファイルをダウンロードする:**    
**セットアップ ダウンローダー** を使って、System Center Configuration Manager の前提条件の再頒布可能ファイル、言語パック、製品の最新の更新プログラムをダウンロードします。  

詳細については、「[セットアップ ダウンローダー](/sccm/core/servers/deploy/install/setup-downloader)」を参照してください。  

**サーバーとクライアントの言語の管理を計画する**  
サイトのアップグレード時には、アップグレード中に選択した言語パックのバージョンのみがインストールされます。  

-   セットアップでは、サイトの現在の言語構成を確認してから、事前にダウンロードした前提条件ファイルが保存されているフォルダー内の使用可能な言語パックを識別します。  
-   その後で、現在のサーバー言語パックとクライアント言語パックの選択を確認したり、言語のサポートを追加または削除するように選択を変更したりできます。  
-   セットアップの実行時に使用できる言語パック (ダウンロードした前提条件ファイルと一緒に取得したもの) のみを選択することができます。  

> [!NOTE]  
>  System Center 2012 Configuration Manager の言語パックを使用して、System Center Configuration Manager サイトで言語を有効にすることはできません。  

言語パックの詳細については、「[System Center Configuration Manager の言語パック](../../../../core/servers/deploy/install/language-packs.md)」を参照してください。  

**サイトのアップグレードに関する考慮事項を確認する**:  
サイトをアップグレードすると、一部の機能と構成が既定の構成にリセットされます。 この点と、関連する変更に備えるには、「  [アップグレード時の考慮事項](#bkmk_considerations)」の情報をご確認ください。  

**中央管理サイトとプライマリ サイトのサイト データベースのバックアップを作成する:**  
サイトをアップグレードする前に、サイト データベースをバックアップして、障害回復に使用するバックアップを正常に作成できることを確認します。  

「[System Center Configuration Manager のバックアップと回復](../../../../protect/understand/backup-and-recovery.md)」を参照してください。  

**カスタマイズされた Configuration.mof ファイルをバックアップする**:  
ハードウェア インベントリで使用するデータ クラスを定義するためにカスタマイズされた Configuration.mof ファイルを使用する場合は、このファイルのバックアップを作成してから、サイトをアップグレードします。 アップグレード後には、このファイルをサイトに復元します。 このファイルの使用の詳細については、「[System Center Configuration Manager でのハードウェア インベントリの拡張方法](../../../../core/clients/manage/inventory/extend-hardware-inventory.md)」を参照してください。  

**最新のサイト データベース バックアップのコピーで、データベースのアップグレード処理をテストする:**  
Configuration Manager の中央管理サイトやプライマリ サイトをアップグレードする前に、サイト データベースのコピーでサイト データベースのアップグレード処理をテストします。  

-   サイトのアップグレード時にサイト データベースが変更される可能性があるため、サイト データベースのアップグレード処理をテストしておく必要があります  
-   データベースのアップグレード テストは必須ではありませんが、テストによって、実稼働データベースが影響を受ける前に、アップグレードの問題を特定することができます  
-   サイト データベースのアップグレードに失敗すると、サイト データベースが運用不可能になり、機能を復元するにはサイトの回復が必要になることがあります  
-   サイト データベースは階層内のサイト間で共有されますが、各サイトをアップグレードする前に、該当する各サイトのデータベースをテストする計画を立ててください  
-   プライマリ サイトで管理ポイントにデータベース レプリカを使う場合、サイト データベースのバックアップを作成する前にレプリケーションを無効にします  

Configuration Manager では、セカンダリ サイトのバックアップとセカンダリ サイト データベースのテスト アップグレードのいずれもサポートされていません。  

実稼働サイト データベースでテスト データベースのアップグレードを実行することはサポートされていません。 実行するとサイト データベースがアップグレードされ、サイトが機能しなくなる可能性があります。  

詳細については、「 [サイト データベースのアップグレードをテストする](#bkmk_test)」をご覧ください。  

**サイト システムの役割をホストするサイト サーバーと各コンピューターを再起動する**:  
これは、更新プログラムの最後のインストールや前提条件で保留中の操作がないことを確認するために行われる、会社固有の内部プロセスです。  

**サイトをアップグレードする**:  
まず、階層内の最上位サイトで、System Center Configuration Manager ソース メディアから Setup.exe を実行します。  

最上位サイトのアップグレードが完了したら、各子サイトのアップグレードを開始できます。 各サイトのアップグレードが完了してから、次のサイトのアップグレードを開始します。  

階層内のすべてのサイトが System Center Configuration Manager にアップグレードされるまで、階層はバージョンが混在したモードで動作します。  

アップグレードを実行する方法については、「[サイトをアップグレードする](#bkmk_upgrade)」を参照してください。  

### アップグレードの後に
<a id="after-you-upgrade" class="xliff"></a>  
**スタンドアロンの Configuration Manager コンソールをアップグレードする**:  
既定では、中央管理サイトまたはプライマリ サイトをアップグレードする際、インストール時にサイト サーバーにインストールされている Configuration Manager コンソールもアップグレードされます。 ただし、サイト サーバー以外のコンピューターにインストールされている各コンソールは、手動でアップグレードする必要があります。  

> [!TIP]  
>  アップグレードを開始する前に、開いているコンソールを閉じてください。  

詳細については、「[Install System Center Configuration Manager consoles (System Center Configuration Manager コンソールのインストール)](../../../../core/servers/deploy/install/install-consoles.md)」をご覧ください。  

**プライマリ サイトで管理ポイント用のデータベース レプリカを再構成する:**  
プライマリ サイトで管理ポイント用のデータベース レプリカを使用する場合、データベース レプリカをアンインストールしてから、サイトをアップグレードする必要があります。 プライマリ サイトをアップグレードしたら、管理ポイント用のデータベース レプリカを再構成します。   
詳しくは、「  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」をご覧ください。  

**アップグレードの前に無効にしたデータベース メンテナンス タスクを再構成する:**  
アップグレードの前にサイトのデータベースの [System Center Configuration Manager のメンテナンス タスクのリファレンス](../../../../core/servers/manage/reference-for-maintenance-tasks.md)を無効にした場合、アップグレードの前に使用していたのと同じ設定を使用して、サイトでこれらのタスクを再構成します。  

**クライアントをアップグレードする**:  
すべてのサイトを System Center Configuration Manager にアップグレードした後、クライアントのアップグレードを計画します。  

クライアントをアップグレードすると、現在のクライアント ソフトウェアはアンインストールされ、新しいクライアント ソフトウェア バージョンがインストールされます。 クライアントのアップグレードには、Configuration Manager がサポートするどの方法でも使うことができます。  

> [!TIP]  
>  最上位サイトの階層をアップグレードすると、その階層内の各配布ポイントにあるクライアント インストール パッケージも更新されます。 プライマリ サイトをアップグレードすると、そのプライマリ サイトから使用できるクライアント アップグレード パッケージは更新されます。  

既存のクライアントをアップグレードする方法と新しいクライアントをインストールする方法については、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」をご覧ください。  

##  <a name="bkmk_considerations"></a> アップグレード時の考慮事項  
**自動アクション**:  
System Center Configuration Manager にアップグレードすると、自動的に次のアクションが行われます。  

-   すべてのサイト システムの役割の再インストールなど、サイトのリセットが実行されます。  
-   サイトが階層の最上位サイトの場合、その階層内の各配布ポイントでクライアント インストール パッケージが更新されます。 また、Windows アセスメント & デプロイメント キット 10 に含まれている新しい Windows PE バージョンを使うように、サイトで既定のブート イメージが更新されます。 ただし、アップグレードでは、イメージの展開で使用するための既存のメディアはアップグレードされません。  
-   サイトがプライマリ サイトの場合、そのサイトのクライアント アップグレード パッケージが更新されます。  

**アップグレード後の管理ユーザーの手動操作**   
サイトをアップグレードしたら、必ず次の操作を実行してください。  

-   各プライマリ サイトに割り当てられているクライアントがアップグレードされ、新しいバージョンのクライアント ソフトウェアがインストールされていることを確認します。  
-   サイトに接続し、サイト サーバーのリモート コンピューターで実行されている各 Configuration Manager コンソールをアップグレードします。  
-   管理ポイント用にデータベース レプリカを使うプライマリ サイトで、データベース レプリカを再構成します。  
-   サイトのアップグレード後は、CD および DVD の ISO ファイルや USB フラッシュ ドライブ、Windows To Go の展開で使用されたかハードウェア ベンダーに提供された事前設定メディアなどの、物理メディアを手動でアップグレードする必要があります。 サイトのアップグレードでは、既定のブート イメージが更新されますが、これらのメディア ファイルや外部で使用されたデバイスを Configuration Manager にアップグレードすることはできません。  
-   Windows PE の元の (古い) バージョンを必要としないときに、既定以外のブート イメージの更新を計画してください。  

**構成と設定に影響がある操作**   
サイトを System Center Configuration Manager にアップグレードすると、一部の構成と設定はアップグレード後に無効になるか、新しい既定の構成に設定されます。 保持されない設定や変化する設定を次の表に示します。サイトのアップグレード時の設定を計画するのに役立つ詳細も提供します。  

-   **ソフトウェア センター:**  
    次のソフトウェア センター項目が既定値にリセットされます。  
    -   [**勤務先情報** ] は、月曜日から金曜日の **午前 5 時** から **午後 10 時** Monday から Friday.  
    -   [ **コンピューターのメンテナンス** ] の値は [ **コンピューターがプレゼンテーション モードのときはソフトウェア センターを停止する**] に設定されます。  
    -   [ **リモート コントロール** ] の値は、そのコンピューターに割り当てられているクライアント設定の値に設定されます。  
-   **ソフトウェア更新プログラムの概要作成スケジュール：**  
     ソフトウェア更新プログラムやソフトウェア更新プログラム グループ用のカスタムの概要スケジュールは、1 時間という既定値にリセットされます。 アップグレードが完了した後に、カスタムの概要値を目的の頻度にリセットしてください。  

##  <a name="bkmk_test"></a> サイト データベースのアップグレードをテストする  
次の情報は、System Center 2012 Configuration Manager などの以前のバージョンを System Center Configuration Manager にアップグレードする場合にのみ適用されます。

サイトをアップグレードする前に、そのサイトのデータベースのコピーでアップグレードをテストします。  

データベースでアップグレードをテストするために、まず、サイト データベースのコピーを Configuration Manager サイトをホストしていない SQL Server インスタンスに復元します。 データベースのコピーをホストするのに使用している SQL Server のバージョンが、データベースのコピーのソースである Configuration Manager のバージョンがサポートしている SQL Server のバージョンである必要があります。  

次に、サイト データベースを復元した後、SQL Server コンピューターで、System Center Configuration Manager 用のソース メディア フォルダーから、**/TESTDBUPGRADE** コマンド ライン オプションを使って Configuration Manager のセットアップを実行します。  

-   サイト データベースのバックアップの作成方法と復元方法については、「[セットアップに使用されるコマンドライン オプション](../../../../core/servers/deploy/install/command-line-options-for-setup.md)」をご覧ください。  
-   **/TESTDBUPGRADE** コマンド ライン オプションの詳細については、「[セットアップに使用されるコマンドライン オプション](../../../../core/servers/deploy/install/command-line-options-for-setup.md)」にある表をご覧ください。  
-   サポートされている SQL Server のバージョンの詳細については、「[System Center Configuration Manager の SQL Server バージョンのサポート](../../../../core/plan-design/configs/support-for-sql-server-versions.md)」トピックを参照してください。  

> [!TIP]  
>  Microsoft Intune と Configuration Manager を統合する場合:  
>   
>  5 日以上前のサイト データベースのコピーに対してデータベース アップグレードのテストを実行すると、次のいずれかのメッセージを受け取ることがあります:  
>   
>  -   警告: アップグレードするとクラウドへの完全同期が実行されます。  
>  -   エラー: データベースをアップグレードするとクラウドへの完全同期が実行されます。  
>   
> どちらも、アップグレード テストの失敗や問題を示すものではないため、データベース アップグレードのテスト中には無視してかまいません。 これは、実際のアップグレード中に **Cloud** データベース レプリケーション グループからのデータが Microsoft Intune と同期される可能性があることを示しています。  

アップグレードを計画している各中央管理サイトとプライマリ サイトで、以下の手順に従います。  

#### サイト データベースのアップグレードをテストするには
<a id="to-test-a-site-database-for-upgrade" class="xliff"></a>  

1.  サイト データベースのコピーを作成してから、サイト データベースと同じエディションを使用しており、Configuration Manager サイトをホストしていない SQL Server インスタンスにこのコピーを復元します。 たとえば、サイト データベースで SQL Server Enterprise Edition のインスタンスを実行している場合、同様に SQL Server Enterprise Edition を実行している SQL Server インスタンスにデータベースを復元します。  

2.  データベースのコピーを復元した後で、新しいバージョンの System Center Configuration Manager のソース メディアからセットアップを実行します。 セットアップを実行する際は、 **/TESTDBUPGRADE** コマンド ライン オプションを使います。 データベースのコピーをホストしている SQL Server インスタンスが既定のインスタンスでない場合は、コマンド ライン引数を指定してサイト データベースのコピーをホストしているインスタンスを特定することも必要になります。  

     たとえば、SMS_ABC というデータベース名のサイト データベースをアップグレードすることを計画しているとします。 このサイト データベースのコピーを、DBTest というインスタンス名のサポートされている SQL Server インスタンスに復元します。 サイト データベースのこのコピーのアップグレードをテストするには、次のコマンド ラインを使います: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Setup.exe は、System Center Configuration Manager のソース メディアの **SMSSETUP\BIN\X64** にあります。  

3.  データベースのアップグレード テストを実行する SQL Server インスタンスで、システム ドライブのルート内の ConfigMgrSetup.log を確認し、進行状況と成功状態を監視します。  

    -   テスト アップグレードが失敗した場合、サイト データベースのアップグレードの失敗に関連する問題を解決し、サイト データベースの新しいバックアップを作成してから、サイト データベースの新しいコピーのアップグレードをテストします。  
    -   プロセスが成功したら、データベース コピーを削除できます。  

        > [!NOTE]  
        >  テスト アップグレードに使用したサイト データベースのコピーを復元して、任意のサイトのサイト データベースとして使用することはサポートされていません。  

サイト データベースのコピーのアップグレードが成功したら、Configuration Manager サイトとそのサイト データベースのアップグレードに進みます。  

##  <a name="bkmk_upgrade"></a> サイトをアップグレードする  
サイトのアップグレード前の構成を完了して、データベースのコピーでサイト データベースのアップグレードをテストし、インストールを計画しているサービス パック バージョンの前提条件ファイルと言語パックをダウンロードしたら、Configuration Manager サイトをアップグレードできるようになります。  

階層内のサイトをアップグレードする際、まず、階層の最上位サイトをアップグレードします。 この最上位サイトは、中央管理サイトまたはスタンドアロンのプライマリ サイトのいずれかです。 中央管理サイトのアップグレードが完了した後で、任意の順序で子プライマリ サイトをアップグレードできます。 プライマリ サイトをアップグレードした後で、そのサイトの子セカンダリ サイトをアップグレードするか、セカンダリ サイトをアップグレードする前に他のプライマリ サイトをアップグレードできます。  

中央管理サイトやプライマリ サイトをアップグレードするには、System Center Configuration Manager のソース メディアからセットアップを実行します。 ただし、セカンダリ サイトをアップグレードする際、セットアップは実行しません。 代わりに、プライマリ親サイトのアップグレードが完了した後で、Configuration Manager コンソールを使用してセカンダリ サイトをアップグレードします。  

サイトをアップグレードする前に、サイトのアップグレードが完了するまで、サイト サーバーにインストールされている Configuration Manager コンソールを閉じます。 また、サイト サーバー以外のコンピューターで実行されている各 Configuration Manager コンソールも閉じます。 サイトのアップグレードが完了した後で、コンソールを再接続できます。 ただし、Configuration Manager コンソールを新しいバージョンの Configuration Manager にアップグレードするまで、新しいバージョンの Configuration Manager で使用できる一部のオブジェクトと情報をコンソールに表示できません。  

Configuration Manager サイトをアップグレードするには、次の手順に従います。  

#### 中央管理サイトまたはプライマリ サイトをアップグレードするには
<a id="to-upgrade-a-central-administration-site-or-primary-site" class="xliff"></a>  

1.  セットアップを実行するユーザーが、次のセキュリティ権限を持っていることを確認します。  

    -   サイト サーバー コンピューターのローカル管理者権限  
    -   サイトがリモートの場合は、そのリモート サイト データベース サーバーのローカル管理者権限    </br></br>

2.  サイト サーバー コンピューターでエクスプローラーを開き、**&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64** に移動します。  

3.  **Setup.exe**をダブルクリックします。 Configuration Manager のセットアップ ウィザードが起動します。  

4.  [ **開始する前に** ] ページで [ **次へ**] をクリックします。  

5.  [ **はじめに** ] ページで [ **Configuration Manager サイトをアップグレードする**] を選択してから、[ **次へ**] をクリックします。  

6.  [ **プロダクト キー** ] ページで [ **次へ**] をクリックします。  

     以前に Configuration Manager 評価版をインストールした場合、[**この製品の製品版をインストール**] を選択し、Configuration Manager の完全インストール用のプロダクト キーを入力して、サイトを完全なバージョンに変換できます。  

     System Center Configuration Manager については、2016 年 10 月リリースのバージョン 1606 基準メディア以降、ソフトウェア アシュアランス契約の有効期限の日付を指定できます。 ライセンス契約の**ソフトウェア アシュアランスの有効期限**を通知する便利なアラームとして、この日付を指定することもできます。 セットアップ時に入力しなかった場合は、後で Configuration Manager コンソール内から指定できます。

     >  [!NOTE]   
     >  Microsoft では、お客様が入力した有効期限の日付を確認していません。また、ライセンスを検証する場合もこの日付を使用しません。  お客様は有効期限を通知するアラームとして、この日付を使用することができます。 Configuration Manager ではオンラインで新しいソフトウェア更新プログラムが提供されていないか定期的に確認します。このような追加の更新プログラムを取得するためにはソフトウェア アシュアランス ライセンスが最新の状態になっている必要があります。このため有効期限を通知するアラーム機能は便利です。    

     詳細については、「[System Center Configuration Manager のライセンスとブランチ](/sccm/core/understand/learn-more-editions)」を参照してください。

7.  [ **マイクロソフト ソフトウェア ライセンス条項** ] ページで、ライセンス条項を読んで同意し、[ **次へ**] をクリックします。  

8.  [ **必須ライセンス** ] ページで、必須ソフトウェアのライセンス条項を読んで同意し、[ **次へ**] をクリックします。 ソフトウェアがダウンロードされ、必要に応じて、サイト システムまたはクライアントに自動的にインストールされます。 次のページに進む前に、すべてのチェック ボックスをオンにする必要があります。  

9. [ **必須ファイルのダウンロード** ] ページで、前提条件の最新の再頒布可能ファイル、言語パック、および製品の最新の更新プログラムをインターネットからダウンロードするか、以前にダウンロードしたファイルを使用するかを指定し、[ **次へ**] をクリックします。 セットアップ ダウンローダーを使用して既にファイルをダウンロードしている場合は、[ **ダウンロード済みのファイルを使用する** ] を選択して、ダウンロード先フォルダーを指定します。 詳細については、「[セットアップ ダウンローダー](/sccm/core/servers/deploy/install/setup-downloader)」を参照してください。

    > [!NOTE]  
    >  前にダウンロードしたファイルを使用する場合は、ダウンロード先フォルダーに、最新バージョンのファイルが含まれていることを確認してください。  

10. [サーバーの言語の選択] ページで、サイトに現在インストールされている言語の一覧を表示します。 **** このサイトで Configuration Manager コンソールとレポートに使用できるようにする追加の言語を選択するか、このサイトでサポートする必要がなくなった言語をクリアして、[**次へ**] をクリックします。 既定では英語が選択され、選択を解除することはできません。  

    > [!IMPORTANT]  
    >  Configuration Manager の各バージョンで、以前のバージョンの Configuration Manager の言語パックは使用できません。 アップグレードする Configuration Manager サイトで言語のサポートを有効にするには、その新しいバージョンの言語パック バージョンを使用する必要があります。 たとえば、System Center 2012 Configuration Manager から System Center Configuration Manager へのアップグレード中に、System Center Configuration Manager バージョンの言語パックが、ダウンロードした前提条件ファイルで使用できない場合、その言語のサポートをインストールすることはできません。  

11. [クライアント言語の選択] ページで、サイトに現在インストールされている言語の一覧を表示します。 **** このサイトでクライアント コンピューターに使用できるようにする追加の言語を選択するか、このサイトでサポートする必要がなくなった言語をクリアします。 モバイル デバイス クライアントのすべてのクライアント言語を有効にするかどうかを指定して、[ **次へ**] をクリックします。 既定では英語が選択され、選択を解除することはできません。  

    > [!IMPORTANT]  
    >  Configuration Manager の各バージョンで、以前のバージョンの Configuration Manager の言語パックは使用できません。 アップグレードする Configuration Manager サイトで言語のサポートを有効にするには、その新しいバージョンの言語パック バージョンを使用する必要があります。 たとえば、System Center 2012 Configuration Manager から System Center Configuration Manager へのアップグレード中に、System Center Configuration Manager バージョンの言語パックが、ダウンロードした前提条件ファイルで使用できない場合、その言語のサポートをインストールすることはできません。  

12. [ **設定の概要** ] ページで、[ **次へ** ] をクリックして前提条件チェッカーを起動し、サイトをアップグレードするサーバーの準備ができているかどうかを確認します。  

13. [ **インストールの前提条件チェック** ] ページに問題が何も表示されていない場合は、[ **次へ** ] をクリックして、プライマリ サイトとサイト システムの役割をアップグレードします。 一覧に問題が表示されている場合は、その問題をクリックして解決方法を確認します。 セットアップを続行する前に、一覧内でステータスが [エラー] になっているすべての問題を解決します。 **** 問題を解決したら、[ **前提条件チェックの実行** ] をクリックして、もう一度前提条件チェックを実行します。 システム ドライブのルートにある ConfigMgrPrereq.log ファイルを開いて、前提条件チェッカーの結果を確認することもできます。 ログ ファイルには、ユーザー インターフェイスに表示されていない情報が含まれていることがあります。 インストールの前提条件チェックの規則と説明の一覧については、「[前提条件チェッカー](/sccm/core/servers/deploy/install/list-of-prerequisite-checks)」を参照してください。  

[アップグレード] ページに、進行状況の全体的なステータスが表示されます。 **** コア サイト サーバーとサイト システムのインストールが完了したら、ウィザードを閉じることができます。 サイトの構成がバックグラウンドで続行されます。  

#### セカンダリ サイトをアップグレードするには
<a id="to-upgrade-a-secondary-site" class="xliff"></a>  

1.  セットアップを実行する管理ユーザーが、次のセキュリティ権限を持っていることを確認します。  

    -   セカンダリ サイト コンピューターのローカル管理者権限  
    -   親プライマリ サイトのインフラストラクチャ管理者または完全な権限を持つ管理者のセキュリティ ロール  
    -   セカンダリ サイトのサイト データベースのシステム管理者 (SA) の権限  
    </br>
2.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

3.  [ **管理** ] ワークスペースで [ **サイトの構成**] を展開して、[ **サイト**] をクリックします。  

4.  アップグレードするセカンダリ サイトを選択し、[ **ホーム** ] タブの [ **サイト** ] グループで、[ **アップグレード**] をクリックします。  

5.  [はい] をクリックして決定を確認し、セカンダリ サイトのアップグレードを開始します。 ****  

セカンダリ サイトのアップグレードは、バックグラウンドで進行します。 アップグレードが完了した後で、Configuration Manager コンソールでステータスを確認できます。 ステータスを確認するには、セカンダリ サイト サーバーを選択して、[ **ホーム** ] タブの [ **サイト** ] グループにある [ **インストール ステータスの表示**] をクリックします。  

##  <a name="BKMK_PostUpgrade"></a> アップグレード後のタスクを実行する  
サイトを新しいサービス パックにアップグレードした後で、サイトのアップグレードまたは再構成を終了するために、追加のタスクを完了することが必要になる場合があります。 このようなタスクには、Configuration Manager クライアントまたは Configuration Manager コンソールのアップグレード、管理ポイントのデータベース レプリカの再有効化、サービス パックのアップグレード後は保持されない、使用する Configuration Manager 機能の設定の復元などがあります。  

**セカンダリ サイトの既知の問題:**  
- **バージョン 1511 にアップグレードする場合:** セカンダリ サイトのクライアントがセカンダリ サイトから管理ポイント (プロキシ管理ポイント) を検索できるようにするには、セカンダリ サイトの配布ポイントも含む境界グループに管理ポイントを手動で追加します。  

- **バージョン 1606 以降にアップグレードする場合:** プロキシ管理ポイントは、セカンダリ サイトの配布ポイントを含む境界グループに自動的に追加されます。

