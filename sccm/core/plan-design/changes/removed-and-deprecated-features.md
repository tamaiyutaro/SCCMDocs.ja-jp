---
title: "非推奨の機能 |Microsoft Docs"
description: "System Center Configuration Manager でサポートされなくなった機能、製品、およびオペレーティング システムについて説明します。"
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e23acf743d8f73afd213c44c3728d1b66d7e558f
ms.contentlocale: ja-jp
ms.lasthandoff: 06/28/2017


---
# System Center Configuration Manager から削除された機能と非推奨の機能
<a id="removed-and-deprecated-features-for-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager のサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の機能、製品、およびオペレーティング システムについて説明します。 これは、Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は、今後のリリースで変更される可能性があります。また、非推奨の機能、製品、またはオペレーティング システムをすべて記載しているわけではありません。  

## この情報の使用方法
<a id="how-to-use-this-information" class="xliff"></a>  
機能またはオペレーティング システムが非推奨と最初に示されるとき、それは今後の Configuration Manager のバージョンで、それの Configuration Manager での使用がサポートされなくなることを意味します。 この情報は、その機能またはオペレーティング システムの代わりとなるものを計画できるよう、提供しています。 それがサポート対象外となる Configuration Manager の最初のバージョンがリリースされると、その特定のバージョンを示すよう、このトピックは更新されます。  

機能またはオペレーティング システムがサポート対象外となった場合でも、前のバージョンのサポート対象の Configuration Manager を使用する場合、その機能またはオペレーティング システムはサポートされます。 ただし、それ以降の日付にリリースされたまたは記載されているバージョンの Configuration Manager を使用する場合、そのバージョンの Configuration Manager ではサポートされません。

例: ある機能が 2016 年 9 月以降にリリースされる更新プログラムからサポート対象外となる予定の場合、その機能は 2016 年 10 月にリリースされる更新 1610 には含まれません。
-  更新 1610 では、この機能はサポートされません。
-  このトピックは更新され、バージョン 1610 でサポート対象外となることが明記されます。
ただし、その機能をサポートする 1602 や 1606 などの以前のバージョンを使用する場合、使用しているバージョンがサポート対象外となるまで、その機能は使用し続けられます。

詳細については、次をご覧ください。
 - [Microsoft サポート ライフサイクル](https://support.microsoft.com/lifecycle) Web サイト
 - [Configuration Manager の Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)




## 非推奨オペレーティング システム
<a id="deprecated-operating-systems" class="xliff"></a>
### サーバー オペレーティング システム
<a id="server-operating-systems" class="xliff"></a>  

|**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除** |  
|-|-|-|  
|Windows Server 2008|2015 年 7 月 10 日|バージョン 1511 </br></br>サイト システムとしてのサポートは削除されています  (注 1 をご覧ください)。|  
|Windows Server 2008 R2|2015 年 7 月 10 日| バージョン 1702 (注 2 を参照)|  

-   注 1: このオペレーティング システムは、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 このサポートの廃止が発表されるまで、またはこのオペレーティング システムの拡張サポート期間が終了するまでは、このオペレーティング システムを配布ポイントとして使用し続けることができます。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

-   注 2: バージョン 1702 以降では、このオペレーティング システムはサイト サーバーやほとんどのサイト システムの役割でサポートされていません。ただし、1702 より前のバージョンで引き続き使用することはできます。 このサポートの廃止が発表されるまで、またはこのオペレーティング システムの延長サポート期間が終了するまで、配布ポイントのサイト システムの役割 (プル配布ポイント、PXE およびマルチキャストの場合を含む) に対してこのオペレーティング システムは引き続きサポートされます。 バージョン 1602 より、サイト サーバーのオペレーティング システムを Windows Server 2008 R2 から Windows Server 2012 R2 にインプレース アップグレードできます。  

     サイト サーバーのオペレーティング システムのインプレース アップグレードに関する詳細については、「[System Center Configuration Manager の変更点](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)」の「[Windows Server 2008 R2 を実行するサイト サーバーのオペレーティング システムのインプレース アップグレード](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS)」セクションを参照してください。



### クライアント オペレーティング システム
<a id="client-operating-systems" class="xliff"></a>  

 特に明記されていない限り、Configuration Manager クライアントとしてサポートされている各オペレーティング システムは、オペレーティングシステムの延長サポート終了日までサポートされます。 延長サポート終了日の詳細については、「[Microsoft サポート ライフ サイクル](https://support.microsoft.com/lifecycle)」を参照してください。 延長サポート終了日より前にオペレーティング システムの Configuration Manager のサポートが終了する場合は、そのオペレーティング システムの廃止日とサポート削除日がここに表示されます。  

|**オペレーティング システム**|**最初に非推奨と発表**|**サポートの削除**|  
|-|-|-|  
|Windows XP|2015 年 7 月 10 日|バージョン 1511|  
|Windows XP Embedded|2015 年 7 月 10 日|バージョン 1702|  
|Windows Server 2003|2015 年 7 月 10 日|バージョン 1511|  
|Windows Server 2003 R2|2015 年 7 月 10 日|バージョン 1511|  
|Windows Vista|2015 年 7 月 10 日|バージョン 1511|  
|Mac OS X 10.6 - 10.8|2015 年 7 月 10 日|バージョン 1511|  
|Windows Mobile 6.0 - 6.5|2015 年 7 月 10 日|バージョン 1511|  
|Nokia Symbian Belle|2015 年 7 月 10 日|バージョン 1511|  
|Windows CE 5.0 - 6.0|2015 年 7 月 10 日|バージョン 1511|  


## サイト データベースとしてのサポートが廃止された SQL Server バージョン
<a id="deprecated-support-for-sql-server-versions-as-a-site-database" class="xliff"></a>  

|**SQL Server バージョン**|**最初に非推奨と発表**|**サポートの削除**|   
|-|-|-|  
|SQL Server 2008|2015 年 7 月 10 日|バージョン 1511|  
|SQL Server 2008 R2|2015 年 7 月 10 日|バージョン 1702|  

使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法 (簡単な方法から順に示されています) を使用することをお勧めします。
1. [SQL Server をインプレースでアップグレードします](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (推奨)。
2. 新しいコンピューターに新しいバージョンの SQL Server をインストールしてから、Configuration Manager セットアップの[データベースの移動オプションを使用](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)して、サイト サーバーを新しい SQL Server にポイントします。
3. [バックアップと回復](/sccm/protect/understand/backup-and-recovery)を使用します。


## 非推奨の機能
<a id="deprecated-features" class="xliff"></a>  

|**機能**|**最初に非推奨と発表**|**サポートの削除**|  
|-|-|-|  
|ネットワーク アクセス保護 (NAP) - System Center 2012 Configuration Manager の機能|2015 年 7 月 10 日|バージョン 1511|  
|帯域外管理 - System Center 2012 Configuration Manager の機能|2015 年 10 月 16 日|バージョン 1511|
|タスク シーケンス: <br /> - OSDPreserveDriveLetter  <br /><br /> 既定で、オペレーティング システムの展開中に、Windows セットアップが使用する最適なドライブ文字を決定するようになりました (通常は C:)。 別のドライブを使用するように指定する場合は、オペレーティング システムの適用タスク シーケンスのステップで場所を変更できます。 [**このオペレーティング システムの適用先を選択してください。**] 設定に移動し、[**特定の論理ドライブ文字**] を選択し、使用するドライブを選択します。 |2016 年 6 月 20 日 |バージョン 1606 |
|タスク シーケンス: <br /> - ディスクをダイナミックに変換 <br /> - 展開ツールのインストール |2016 年 11 月 18 日|2017 年 6 月 1 日以降にリリースされる最初の更新プログラムでこれらのタスク シーケンスのサポートは終了します。|
|ソフトウェア センターは新しい現代的な外観へと一新されます。 Silverlight を使用するアプリケーション カタログにしか表示されなかったアプリ (ユーザーが利用できるアプリ) がソフトウェア センターの **[アプリケーション]** タブに表示されるようになります。 アプリケーション カタログには、ソフトウェア センターの **[インストールのステータス]** タブ上にあるリンクを使用してアクセスできます。<br><br>以前のバージョンのソフトウェア センターは、今後数か月の間に使用できなくなります。<br><br>新しいソフトウェア センターを使用するようにクライアントをセットアップするには、クライアント設定 **[コンピューター エージェント]** > **[新しいソフトウェア センターの使用]** を有効化します。<br><br>ソフトウェア センターの詳細については、「[System Center Configuration Manager のアプリケーション管理の計画と構成](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management)」を参照してください。|2016 年 12 月 13 日|ソフトウェア センターの以前のバージョンは、2018 年 1 月 1 日以降にリリースされる最初の更新プログラムによってサポートが終了します。|
|Configuration Manager によるバーチャル ハード ディスク (VHD) の管理。 </br></br>これには、新しい VHD の作成オプション、またはタスク シーケンスを使用した VHD の管理オプションの削除と、Configuration Manager コンソールからのバーチャル ハード ディスクのノードの削除が含まれます。 </br></br>このサポートが削除されると、既存の VHD は削除されませんが、Configuration Manager コンソール内からアクセスできなくなります。  |2017 年 1 月 6 日 |VHD のサポートは、2017 年 6 月 1 日より後にリリースされた最初の更新プログラムで終了します。|
|System Center Configuration Manager Upgrade Assessment Tool。 </br></br>Upgrade Assessment Tool は、System Center Configuration Manager と Application Compatibility Toolkit (ACT) 6.x の両方に依存します。 ACT の最終バージョンは、Windows 10 v1511 ADK に同梱されていました。 今後、ACT が更新されることはないため、Upgrade Assessment Tool のサポートは廃止されます。 </br></br>Upgrade Assessment Tool は、[アップグレードの準備](/sccm/core/clients/manage/upgrade/upgrade-analytics)機能に置き換えられます。 非推奨に関する注記は、9/12/2016 に [UAT のダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=37145)に追加されました。 |9/12/2016  | 2017 年 7 月 11 日 |  


<br></br>
バージョン 1511 の System Center Configuration Manager リリースで削除された機能の詳細を次に示します。

###  <a name="bkmk_amt"></a> 帯域外管理  
 Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。  

-   [Microsoft System Center Configuration Manager 用 Intel SCS アドオン](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。 アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

-   System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。  

###  <a name="bkmk_nap"></a> ネットワーク アクセス保護  
 System Center Configuration Manager では、ネットワーク アクセス保護のサポートが削除されました。 この機能は Windows Server 2012 R2 で非推奨となり、Windows 10 からは削除されています。  

 ネットワーク アクセス保護の代替方法については、「 *ネットワーク ポリシーとアクセス サービスの概要* 」で [非推奨の機能](https://technet.microsoft.com/library/hh831683.aspx)に関する説明を参照してください。

