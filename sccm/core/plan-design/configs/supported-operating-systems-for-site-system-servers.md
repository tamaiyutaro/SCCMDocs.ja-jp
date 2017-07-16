---
title: "サポートされるサイト システム サーバー | Microsoft Docs"
description: "System Center Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。"
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: be635e4df79b57b6f650287fa3774d2c10613cee
ms.contentlocale: ja-jp
ms.lasthandoff: 06/28/2017


---
# System Center Configuration Manager サイト システム サーバーのサポートされるオペレーティング システム
<a id="supported-operating-systems-for-system-center-configuration-manager-site-system-servers" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*


この記事では、System Center Configuration Manager サイトまたはサイト システムの役割をホストできる Windows バージョンについて説明します。


このトピックの情報は、次の記事の情報とともに使用します。
-   [Configuration Manager の推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)
-   [Configuration Manager のサイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Configuration Manager のサイズとスケール番号](../../../core/plan-design/configs/size-and-scale-numbers.md)



## Windows Server 2016: Standard、Datacenter
<a id="windows-server-2016-standard-and-datacenter" class="xliff"></a>
バージョン 1606 以降および KB3186654 以降の修正プログラム ロールアップ (2016 年 10 月にリリースされた 1606 のベースライン バージョン) により、このオペレーティング システムは次の用途に対応します。

**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント

## Windows Server 2012 R2 (x64): Standard、Datacenter
<a id="windows-server-2012-r2-x64-standard-and-datacenter" class="xliff"></a>  
**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## Windows Server 2012 (x64): Standard、Datacenter
<a id="windows-server-2012-x64-standard-and-datacenter" class="xliff"></a>  
**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## Windows Server 2008 R2 SP1 (x64): Standard、Enterprise、Datacenter
<a id="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter" class="xliff"></a>  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 R2 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートの詳細については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

 Configuration Manager バージョン 1702 以降では、このオペレーティング システムはサイト サーバーやほとんどのサイト システムの役割でサポートされませんが、配布ポイントのサイト システムの役割 (プル配布ポイント、PXE およびマルチキャストの場合を含む) では引き続きサポートされます。

 1702 より前のバージョンでは、以下の使用が引き続きサポートされます。


**サイト サーバー:**  

-   中央管理サイト  

-   プライマリ サイト  

-   セカンダリ サイト  

**サイト システム サーバー:**  

-   アプリケーション カタログ Web サービス ポイント  

-   アプリケーション カタログ Web サイト ポイント  

-   資産インテリジェンス同期ポイント  

-   証明書登録ポイント  

-   配布ポイント  

     配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

-   Endpoint Protection ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

-   フォールバック ステータス ポイント  

-   管理ポイント

-   レポート サービス ポイント  

-   サービス接続ポイント  

-   サイト データベース サーバー  

     サイト データベース サーバーは、読み取り専用のドメイン コントローラー (RODC) ではサポートされていません。 詳細については、Microsoft サポート技術情報の「 [You may encounter problems when installing SQL Server on a domain controller (ドメイン コントローラーに SQL Server をインストールすると問題が発生する)](http://go.microsoft.com/fwlink/p/?LinkId=264856) 」を参照してください。 さらに、セカンダリ サイト サーバーは、ドメイン コントローラーではサポートされません。  

-   SMS_Provider  

-   ソフトウェアの更新ポイント  

-   状態移行ポイント  

## Windows Server 2008 SP2 (x86, x64): Standard、Enterprise、Datacenter
<a id="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter" class="xliff"></a>  
 [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)で詳述するように、Windows Server 2008 が延長サポートになり、メインストリーム サポートが終了しました。 Configuration Manager を使用したサイト システム サーバーとしてのこれらのオペレーティング システムの将来のサポートの詳細については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

このオペレーティング システムは、サイト サーバーとして、または配布ポイントとプル配布ポイントを除くサイト システムの役割としてはサポートされていません。 このサポートの廃止が発表されるまで、またはこのオペレーティング システムの拡張サポート期間が終了するまでは、このオペレーティング システムを配布ポイントとして使用し続けることができます。 詳細については、「[Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095)」 (Windows Server 2008 で System Center Configuration Manager CB および LTSB のインストールに失敗する) を参照してください。

**サイト システム サーバー:**  
-   配布ポイント  

    -   このオペレーティング システムの配布ポイントでは、マルチキャストをサポートしません。  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされますが、EFI モードでのクライアント コンピューターのネットワーク ブートはサポートしません。 クライアント コンピューターのレガシ モードでの BIOS ブートまたは EFI ブートはサポートされます。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  



## Windows 10 (x86, x64): Pro、Enterprise
<a id="windows-10-x86-x64-pro-and-enterprise" class="xliff"></a>  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## Windows 8.1 (x86、x64): Professional、Enterprise
<a id="windows-81-x86-x64-professional-and-enterprise" class="xliff"></a>  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## Windows 8 (x86、x64): Professional、Enterprise
<a id="windows-8-x86-x64-professional-and-enterprise" class="xliff"></a>
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

## Windows 7 SP1 (x86、x64): Professional、Enterprise、Ultimate
<a id="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate" class="xliff"></a>  
**サイト システム サーバー:**  

-   配布ポイント  

    -   このオペレーティング システムの配布ポイントは、PXE ではサポートされません。  

    -   このオペレーティング システムのバージョンの配布ポイントでは、マルチキャストをサポートしません。  

    -   配布ポイントは、それぞれに異なる要件を持つ複数の異なる構成をサポートします。 場合によっては、これらの構成は、サーバー上のインストールだけでなく、クライアント オペレーティング システム上のインストールをサポートします。 配布ポイントで使用可能なオプションの詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  


## Windows Server 2016 の Server Core インストール
<a id="the-server-core-installation-of-windows-server-2016" class="xliff"></a>
バージョン 1606 以降および KB3186654 以降の修正プログラム ロールアップ (2016 年 10 月にリリースされた 1606 のベースライン バージョン) により、このオペレーティング システムは、配布ポイントとしての用途に対応します。ただし次の制限があります。  
  -   64 ビット バージョンのみがサポートされています。
  -   このオペレーティング システムの配布ポイントでは、PXE またはマルチキャストをサポートしません。  


## Windows Server 2012 R2 の Server Core のインストール
<a id="the-server-core-installation-of-windows-server-2012-r2" class="xliff"></a>  
 記載されている前のオペレーティング システムだけでなく、Windows Server 2012 R2 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。

-   このオペレーティング システムの配布ポイントでは、PXE またはマルチキャストをサポートしません。  

## Windows Server 2012 の Server Core のインストール
<a id="the-server-core-installation-of-windows-server-2012" class="xliff"></a>  
 記載されている前のオペレーティング システムだけでなく、Windows Server 2012 の Server Core インストールが、次の制限付きの配布ポイントとしての使用でサポートされます。  

-   64 ビット バージョンのみがサポートされています。  

-   このオペレーティング システムの配布ポイントでは、PXE またはマルチキャストをサポートしません。

