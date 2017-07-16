---
title: "サービス接続ポイント | Microsoft Docs"
description: "この Configuration Manager サイト システムの役割について学習し、その使用範囲を理解し計画します。"
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.contentlocale: ja-jp
ms.lasthandoff: 06/28/2017


---
# System Center Configuration Manager のサービス接続ポイントについて
<a id="about-the-service-connection-point-in-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager サービス接続ポイントは、階層のいくつかの重要な機能を提供するサイト システムの役割です。 サービス接続ポイントを設定する前に、このサイト システムの役割の設定方法に影響を与える可能性がある使用範囲を理解し、計画を立ててください。  

-   **Microsoft Intune を使用してモバイル デバイスを管理する** – この役割は、Configuration Manager の前のバージョンによって使用される Windows Intune コネクタを置き換え、Intune のサブスクリプションの詳細で構成することができます。 「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../../mdm/understand/hybrid-mobile-device-management.md)」をご覧ください。  

-   **オンプレミス MDM を使用してモバイル デバイスを管理する** – この役割は、インターネットに接続しない管理対象オンプレミス デバイスのサポートを提供します。 「[System Center Configuration Manager でオンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

-   **Configuration Manager インフラストラクチャからの使用データのアップロード** – アップロードする詳細のレベルと量を制御することができます。 アップロードされるデータは、次の点で役立ちます。  

    -   問題の早期識別とトラブルシューティング  

    -   Microsoft の製品やサービスの向上  

    -   使用する Configuration Manager のバージョンに適用する Configuration Manager の更新プログラムの識別  

  各レベルで収集されたデータについて、また、ロールがインストールされた後でコレクションのレベルを変更する方法については、「[System Center Configuration Manager の診断結果と使用状況データ](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)」を参照して、使用する Configuration Manager のバージョンへのリンクをたどります。  

  詳細については、「[使用状況データのレベルと設定](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)」をご覧ください。  

-   **Configuration Manager インフラストラクチャに適用される更新プログラムのダウンロード** – アップロードする使用データに基づいて、インフラストラクチャに関連する更新プログラムのみを入手することができます。  

- **各階層は、この役割の単一インスタンスをサポートします。**  

 -   このサイト システムの役割は、階層の最上位層サイト (中央管理サイトまたはスタンドアロン プライマリ サイト) のみにインストールできます。  

  -   スタンドアロン プライマリ サイトをより大きな階層に拡張する場合、この役割をアンインストールする必要があり、その後、中央管理サイトにインストールすることができます。  


##  <a name="bkmk_modes"></a> 操作モード  
 サービス接続ポイントは、操作の 2 つのモードをサポートしています。  

-   **オンライン モード**。このモードでは、サービス接続ポイントは、更新プログラムの 24 時間ごとの確認と、現在のインフラストラクチャおよび製品バージョンで使用可能な新しい更新プログラムのダウンロードを自動的に行い、Configuration Manager コンソールで使用できるようにします。  

-   **オフライン モード**では、サービス接続ポイントは、Microsoft クラウド サービスに接続しません。そのため、[System Center Configuration Manager のサービス接続ツールを使用して](../../../../core/servers/manage/use-the-service-connection-tool.md)、手動で、使用可能な更新プログラムをインポートする必要があります。  

サービス接続ポイントをインストールした後にオンラインまたはオフラインのモードを変更したら、Configuration Manager SMS_Executive サービスの SMS_DMP_DOWNLOADER スレッドを再起動する必要があります。これにより、この変更が有効になります。 これを行うには、Configuration Manager サービス マネージャーを使用して、SMS_Executive サービスの SMS_DMP_DOWNLOADER スレッドのみを再起動します。 Configuration Manager の SMS_Executive サービスを再起動することもできます (これにより、ほとんどのサイト コンポーネントが再起動されます)。あるいは、サイト バックアップのようにスケジュール タスクを待って、自動的に SMS_Executive サービスを停止後、再起動することもできます。  

Configuration Manager サービス マネージャーを使用するには、コンソールで **[監視]** > **[システムのステータス]** > **[コンポーネントのステータス]** に移動して **[開始]** を選択してから、**[Configuration Manager サービス マネージャー]** を選択します。 サービス マネージャー:  

-   ナビゲーション ウィンドウで、サイトを展開してから **[コンポーネント]** を展開し、再起動するコンポーネントを選択します。  

-   詳細ウィンドウで、コンポーネントを右クリックして、**[クエリ]** を選択します。  

-   コンポーネントのステータスを確認したら、コンポーネントを再び右クリックして、**[停止]** を選択します。  

-   コンポーネントに再び**クエリ**を実行して、コンポーネントが停止していることを確認します。もう一度コンポーネントを右クリックして、**[開始]** を選択します。  

> [!IMPORTANT]  
>  サービス接続ポイントに Microsoft Intune サブスクリプションを追加するプロセスで、サイト システムの役割が自動的にオンラインに設定されます。 サービス接続ポイントは Intune サブスクリプションで設定されている場合にオフライン モードをサポートしません。  

**サイト サーバーからリモートにあるコンピューターに役割をインストールする場合:**  

-   サイト サーバーのコンピューター アカウントは、リモート サービス接続をホストするコンピューターのローカル管理者である必要があります。

-   役割をホストするサイト システム サーバーをサイト システムのインストール アカウントで設定する必要があります。  

-   サイト サーバー上の配布マネージャーは、サイト システムのインストール アカウントを使って、サービス接続ポイントから更新プログラムを転送します。

##  <a name="bkmk_urls"></a> インターネット アクセス要件  
操作を有効にするには、サービス接続ポイントをホストするコンピューター、ならびにそのコンピューターとインターネットの間のファイアウォールにより、通信が**ポート TCP 443** および**ポート TCP 443** を介して次のインターネット上の場所に届くようにする必要があります。 サービス接続ポイントから、これらの場所を利用する際は、Web プロキシ (認証あり、または認証なし) を使用することもできます。  Web プロキシ アカウントを構成する必要がある場合は、「[System Center Configuration Manager でのプロキシ サーバーのサポート](/sccm/core/plan-design/network/proxy-server-support)」を参照してください。

**更新プログラムとサービス**  

-   *.akamaiedge.net  

-   *.akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10 サービス**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## サービス接続ポイントをインストールする
<a id="install-the-service-connection-point" class="xliff"></a>
**[セットアップ]** を実行して階層の最上位サイトをインストールする場合、サービス接続ポイントをインストールするオプションがあります。

[セットアップ] を実行した後、またはサイト システムの役割を再インストールする場合は、**サイト システムの役割の追加**ウィザード、または**サイト システム サーバーの作成**ウィザードを使用して、サーバー上のサイト システムを階層の最上位サイト (中央管理サイトまたはスタンドアロン プライマリ サイト) にインストールします。 どちらのウィザードも、コンソールの **[ホーム]** タブの、**[管理]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** にあります。

## サービス接続ポイントにより使用されるログ ファイル
<a id="log-files-used-by-the-service-connection-point" class="xliff"></a>
Microsoft へのアップロードに関する情報については、サービス接続ポイントを実行するコンピューターの **Dmpuploader.log** をご覧ください。  更新プログラムのダウンロード進捗状況など、ダウンロードについては、**Dmpdownloader.log** をご覧ください。 サービス接続ポイント関連のログの完全な一覧については、Configuration Manager ログ ファイル トピックの「[サービス接続ポイント](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog)」を参照してください。

更新プログラムをダウンロードするプロセスと更新プログラムを他のサイトに複製するプロセスの流れや重要なログ エントリについては、次のフローチャートを使用して理解に役立てることもできます。
 - [フローチャート - 更新プログラムのダウンロード](/sccm/core/servers/manage/download-updates-flowchart)
 - [フローチャート - レプリケーションの更新](/sccm/core/servers/manage/update-replication-flowchart)

