---
title: "LTSB のサポートされている構成 | Microsoft Docs"
description: "System Center Configuration Manager の Long-Term Servicing branch で動作するオペレーティング システムと依存する製品について理解します。"
ms.custom: na
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: b0ba955aa7f854c3fa2c06ccf9ccd8ed354758b0
ms.openlocfilehash: 31bddee83b2365cfa903077ffaa1d7116b194378
ms.contentlocale: ja-jp
ms.lasthandoff: 06/12/2017


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager の Long-Term Servicing Branch のサポートされている構成

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

このトピックの情報を参照して、Configuration Manager の Long-Term Servicing Branch (LTSB) でサポートされるオペレーティング システムと製品の依存関係を理解します。
このトピックまたは LTSB 特定のトピックで特に指定されていない限り、Current Branch バージョン 1606 に適用されるものと同じ構成および制限が、LTSB に適用されます。  競合が発生した場合、使用しているエディションに適用される情報が使用されます。 通常、LTSB は Current Branch よりも制限的です。

## <a name="general-statement-of-support"></a>サポートの概説
この Configuration Manager のブランチでは、次の製品とテクノロジがサポートされています。 ただし、このコンテンツにそれらが含まれていても、その製品の個別のサポート ライフサイクルを超える製品やバージョンのサポートの延長を表すものではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 詳細については、[「マイクロソフト サポート ライフサイクル」](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照し、[「サポート ライフサイクル ポリシーに関する FAQ」](http://go.microsoft.com/fwlink/p/?LinkId=31976)をお読みください。

さらに、次のトピックに示されていない製品および製品バージョンは、[Enterprise Mobility + Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/)で告知されていない限り、サポートされていません。

**今後のサポートに関する制限事項:** LTSB の今後のサーバーとクライアントのオペレーティング システムおよび製品の依存関係は、制限付きでサポートされます。 LTSB のプラットフォーム一覧は、そのリリースの有効期間にわたって固定されます。

**Windows:**
- Windows の品質更新プログラムおよびセキュリティ更新プログラムのみがサポートされます。
- Current Branches (CB)、Current Branch for Business (CBB)、または Windows 10 の LTSB に対してのサポートは追加されません。
-   Windows Server の新しいメジャー バージョンはサポートされていません。

**SQL Server:**
- SQL Server では、品質更新プログラムおよびセキュリティ更新プログラム、または Service Pack のようなマイナー アップグレードのみがサポートされる予定です。
- SQL Server の新しいメジャー バージョンはサポートされません。  

## <a name="site-systems-and-servers"></a>サイト システムおよびサーバー
LTSB では、サイト システムとして次の Windows コンピューターのオペレーティング システムの使用をサポートします。  各オペレーティング システムには、[サイト システム サーバーでサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)の同じエンティティと同じ要件と制限事項があります。  たとえば、Windows 2012 R2 の Server Core のインストール (x64 バージョンである必要があります) では、配布ポイントのホストのみがサポートされ、PXE やマルチキャストはサポートされません。

**サポートされるオペレーティング システム:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard、Datacenter
- Windows Server 2012 (x64): Standard、Datacenter
- Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter
- Windows Server 2008 SP2 (x86、x64): Standard、Enterprise、Datacenter *(注 1 を参照)*
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 8.1 (x86、x64): Professional、Enterprise
- Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate
- Windows Server 2012 の Server Core のインストール
- Windows Server 2012 R2 の Server Core のインストール    

*注 1*: このオペレーティング システムは、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 このサポートの廃止が発表されるまで、またはこのオペレーティング システムの拡張サポート期間が終了するまでは、このオペレーティング システムを配布ポイントとして使用し続けることができます。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

## <a name="client-management"></a>クライアント管理
次のセクションでは、LTSB を使用して管理できるクライアントのオペレーティング システムを確認します。 LTSB では、サポートされるクライアントとして、新しいオペレーティング システムの追加をサポートしません。

### <a name="windows-computers"></a>Windows コンピューター
LTSB を使用して、以下の Windows コンピューター オペレーティング システムと、Configuration Manager に含まれている Configuration Manager クライアント ソフトウェアを管理できます。 詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)」を参照してください。

**サポートされるオペレーティング システム:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard、Datacenter (注 1)
- Windows Server 2012 (x64): Standard、Datacenter (注 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter (注 1)
- Windows Storage Server 2008 R2 (x86、x64): Workgroup、Standard、Enterprise
- Windows Server 2008 SP2 (x86、x64): Standard、Enterprise、Datacenter (注 1)
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 8.1 (x86、x64): Professional、Enterprise
- Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate
- Windows Server 2012 R2 の Server Core のインストール (x64) (注 2)
- Windows Server 2012 の Server Core のインストール (x64) (注 2)
- Windows Server 2008 R2 SP1 の Server Core のインストール (x64)
- Windows Server 2008 SP2 の Server Core のインストール (x86、x64)

**(注 1)**Datacenter リリースは、Configuration Manager でサポートされますが動作は保障されません。  
**(注 2)** クライアント プッシュ インストールをサポートするには、このオペレーティング システムのバージョンを実行するコンピューターで、ファイルおよびストレージ サービスのサーバーの役割のための、ファイル サーバーの役割サービスを実行する必要があります。 Server Core コンピューターに Windows の機能をインストールする詳細については、Windows Server 2012 TechNet ライブラリの「[Server Core サーバーへのサーバーの役割と機能のインストール](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx)」を参照してください。

### <a name="windows-embedded"></a>Windows Embedded
デバイス上にクライアント ソフトウェアをインストールすることによって、LTSB を使用して以下の Windows Embedded デバイスを管理できます。  詳細については、「[System Center Configuration Manager での Windows Embedded デバイスへのクライアント展開の計画](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices)」をご覧ください。

**要件と制限事項**  

-   すべてのクライアント機能は、書き込みフィルターが有効化されていないサポート対象の Windows Embedded システムでサポートされます。  

-   次のいずれかを使用するクライアントは、電源管理以外のすべての機能がサポートされます。  

    -   Enhanced Write Filter (EWF)    

    -   RAM ファイル ベースの書き込みフィルター (FBWF)    

    -   Unified Write Filter (UWF)  

-   アプリケーション カタログは、どのような Windows Embedded デバイスについてもサポートされません。  

-   Windows XP ベースの Windows Embedded デバイスで検出したマルウェアを監視するには、Embedded デバイスに Microsoft Windows WMI スクリプト パッケージを先にインストールしておく必要があります。 このパッケージは、Windows Embedded Target Designer を使用してインストールします。 検出したマルウェアが確実に報告されるようにするには、Embedded デバイスにファイル *WBEMDISP.DLL* および *WBEMDISP.TLB* が存在している必要があり、フォルダー %windir%\System32\WBEM に登録されている必要があります。  

**サポートされるオペレーティング システム:**  
-   Windows 10 Enterprise 2016 LTSB (x86、x64)  
-   Windows 10 Enterprise 2015 LTSB (x86、x64)  
-   Windows Embedded 8.1 Industry (x86、x64)    
-   Windows Thin PC (x86、x64)    
-   Windows Embedded POSReady 7 (x86、x64)    
-   Windows Embedded Standard 7 SP1 (x86、x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Configuration Manager に付属の Configuration Manager モバイル デバイス レガシ クライアントを持つ Windows CE デバイスを管理することができます。  

**要件と制限事項**  

-   モバイル デバイス クライアントには、クライアントをインストールする記憶領域が 0.78 MB 必要です。 モバイル デバイスがサインインするには、さらに最大で 256 KB の追加の記憶領域が必要な場合があります。    

-   これらのモバイル デバイスの機能は、プラットフォームとクライアントの種類によって異なります。 モバイル デバイス レガシ クライアントで Configuration Manager がサポートする管理機能の種類の詳細については、「[System Center Configuration Manager のデバイス管理ソリューションの選択](/sccm/core/plan-design/choose-a-device-management-solution)」を参照してください。  

**サポートされるオペレーティング システム:**  

-   Windows CE 7.0 (ARM および x86 プロセッサ)  

**サポートされる言語:**  
-   中国語 (簡体字、繁体字)    
-   英語 (米国)    
-   フランス語 (フランス)    
-   ドイツ語    
-   イタリア語    
-   日本語  
-   韓国語  
-   ポルトガル語 (ブラジル)  
-   ロシア語  
-   スペイン語 (スペイン)  

### <a name="mac-computers"></a>Mac コンピューター  
 LTSB を使用して、Mac OS X コンピューターを Mac 向けの Configuration Manager クライアントとともに管理できます。

Configuration Manager メディアでは、Mac クライアント インストール パッケージは提供されません。 これは、[Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から、"追加のオペレーティング システム用のクライアント" のダウンロードの一環としてダウンロードできます。  

サポートされている Mac オペレーティング システムは、このセクションに記載されているものに限定されています。 Current Branch の Mac クライアント インストール パッケージへの今後の更新プログラムによってサポートされる可能性のあるその他のオペレーティング システムは、サポート対象には含まれていません。

詳細については、「[How to deploy clients to Macs in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs)」 (System Center Configuration Manager でクライアントを Mac に展開する方法) を参照してください。

**サポートされるバージョン:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Linux および UNIX サーバー
LTSB を使用して、Linux および UNIX サーバーを Linux および UNIX 用の Configuration Manager クライアントとともに管理できます。

Configuration Manager メディアでは、Linux および UNIX クライアント インストール パッケージは提供されません。 これらは、[Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から、追加のオペレーティング システム用のクライアントのダウンロードの一環としてダウンロードできます。 クライアント インストール パッケージに加え、クライアント ダウンロードには、各コンピューター上でクライアントのインストールを管理する install スクリプトも含まれています。

サポートされている Linux および UNIX オペレーティング システムは、このセクションに記載されているものに限定されています。 Current Branch の Linux および UNIX クライアント インストール パッケージへの今後の更新プログラムによってサポートされる可能性のあるその他のオペレーティング システムは、サポート対象には含まれていません。

**要件と制限事項**  

-   Linux および UNIX 向けクライアントのオペレーティング システム ファイルの依存関係を確認するには、[Prerequisites for Client Deployment to Linux and UNIX Servers](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu) (Linux および UNIX サーバーへのクライアントの展開の前提条件) を参照してください。  
-   Linux または UNIX を実行するコンピューターでサポートされている管理機能の概要については、「[How to deploy clients to UNIX and Linux servers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)」 (System Center Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法) を参照してください。  
-   Linux および UNIX のサポートされるバージョンの場合、一覧に示したバージョンには後続のマイナー バージョンがすべて含まれます。 たとえば、CentOS バージョン 6 のサポートが示されている場合は、CentOS 6 の後続のマイナー バージョン (CentOS 6.3 など) もすべて含まれます。 同様に、サービス パックを使用するオペレーティング システム (SUSE Linux Enterprise Server 11 SP1 など) のサポートが示されている場合は、そのオペレーティング システムのバージョンの後続のサービス パックもサポートに含まれます。
-   Linux と UNIX でクライアントをインストールする方法については、「[System Center Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)」を参照してください。


**サポートされるバージョン:**   
次のバージョンは、指定された .tar ファイルを使用してサポートされます。  
### <a name="aix"></a>AIX  

|バージョン|ファイル|  
|-|-|  
|バージョン 5.3 (Power)|ccm-Aix53ppc.&lt;ビルド\>.tar|  
|バージョン 6.1 (Power)|ccm-Aix61ppc.&lt;ビルド\>.tar|  
|バージョン 7.1 (Power)|ccm-Aix71ppc.&lt;ビルド\>.tar|  

### <a name="centos"></a>CentOS  

|バージョン|ファイル|  
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="debian"></a>Debian  

|バージョン|ファイル|    
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 8 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 8 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|バージョン|ファイル|  
|-|-|  
|バージョン 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;ビルド\>.tar|  
|バージョン 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;ビルド\>.tar|  
|バージョン 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;ビルド\>.tar|  
|バージョン 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;ビルド\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|バージョン|ファイル|    
|-|-|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|バージョン|ファイル|  
|-|-|  
|バージョン 4 x86|ccm-RHEL4x86.&lt;ビルド\>.tar|  
|バージョン 4 x64|ccm-RHEL4x64.&lt;ビルド\>.tar|  
|バージョン 5 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 5 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 6 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 6 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 7 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="solaris"></a>Solaris  

|バージョン|ファイル|   
|-|-|  
|バージョン 9 SPARC|ccm-Sol9sparc.&lt;ビルド\>.tar|  
|バージョン 10 x86|ccm-Sol10x86.&lt;ビルド\>.tar|  
|バージョン 10 SPARC|ccm-Sol10sparc.&lt;ビルド\>.tar|  
|バージョン 11 x86|ccm-Sol11x86.&lt;ビルド\>.tar|  
|バージョン 11 SPARC|ccm-Sol11sparc.&lt;ビルド\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|バージョン|ファイル|  
|-|-|  
|バージョン 9 x86|ccm-SLES9x86.&lt;ビルド\>.tar|  
|バージョン 10 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 11 SP1 x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12 x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|バージョン|ファイル|    
|-|-|  
|バージョン 10.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 10.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 12.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x86|ccm-Universalx86.&lt;ビルド\>.tar|  
|バージョン 14.04 LTS x64|ccm-Universalx64.&lt;ビルド\>.tar|  

### <a name="exchange-server-connector"></a>Exchange Server コネクタ
 LTSB は、クライアント ソフトウェアをインストールすることがない、Exchange サーバー インスタンスに接続するデバイスの限定された管理をサポートしています。 詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)」を参照してください。

 **要件と制限事項**  

-   Configuration Manager では、モバイル デバイスを限定的に管理できます。 Exchange Server または Exchange Online を実行しているサーバーに接続する Exchange Active Sync (EAS) 対応デバイス向けに Exchange Server コネクタを使用する場合に、モバイル デバイスは限定的に管理できます。  

-   Exchange Server コネクタが管理するモバイル デバイスで Configuration Manager がサポートする管理機能の詳細については、「[System Center Configuration Manager のデバイス管理ソリューションの選択](/sccm/core/plan-design/choose-a-device-management-solution)」を参照してください。  

**サポートされている Exchange Server のバージョン:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> LTSB では、Exchange Online (Office 365) などのオンライン サービスを通じて接続するデバイスは管理できません。


## <a name="configuration-manager-console"></a>Configuration Manager コンソール
LTSB は、Configuration Manager コンソールを実行するために、次のオペレーティング システムをサポートしています。 .NET Framework 4.6 以上を必要とする Windows 10 を除き、コンソールをホストする各コンピューターは、.NET Framework 4.5.2 以上のバージョンが必要です。

**サポートされるオペレーティング システム:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard、Datacenter
- Windows Server 2012 (x64): Standard、Datacenter
- Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter
- Windows Server 2008 SP2 (x86、x64): Standard、Enterprise、Datacenter
- Windows 10 Enterprise 2016 LTSB (x86、x64)
- Windows 10 Enterprise 2015 LTSB (x86、x64)
- Windows 8.1 (x86、x64): Professional、Enterprise
- Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>サイト データベースとレポート ポイントでサポートされている SQL Server バージョン
LTSB は、サイト データベースとレポート ポイントをホストする SQL Server の次のバージョンをサポートしています。 サポートされている各バージョンで、Current Branch の「[SQL Server バージョンのサポート](/sccm/core/plan-design/configs/support-for-sql-server-versions)」に記載されている同じ構成要件および制限事項が、LTSB に適用されます。  これには、SQL Server クラスター、または SQL Server AlwaysOn 可用性グループの使用が含まれます。  

**サポートされるバージョン:**

- SQL Server 2016: Standard、Enterprise
- SQL Server 2014 SP2: Standard、Enterprise
- SQL Server 2014 SP1: Standard、Enterprise
- SQL Server 2012 SP3: Standard、Enterprise
- SQL Server 2008 R2 SP3: Standard、Enterprise、Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Active Directory ドメインのサポート
すべての LTSB サイト システムは、サポートされている Windows Active Directory ドメインのメンバーであることが必要です。 Active Directory ドメインのサポートは、[Active Directory ドメインのサポート](/sccm/core/plan-design/configs/support-for-active-directory-domains)に記載されるものと同じ要件と制限がありますが、次のドメイン機能レベルに制限されています。

**サポートされているレベル:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Long Term Servicing Branch に適用されるその他のサポートに関するトピック
次の Current Branch トピックの情報は、LTSB に適用されます。
- [サイジングとスケールの数値](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [サイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [高可用性オプション](/sccm/protect/understand/high-availability-options)
- [推奨ハードウェア](/sccm/core/plan-design/configs/recommended-hardware)
- [Windows の機能とネットワークのサポート](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [仮想環境のサポート](/sccm/core/plan-design/configs/support-for-virtualization-environments)

