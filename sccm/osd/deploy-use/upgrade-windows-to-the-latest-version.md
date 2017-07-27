---
title: "Windows を最新バージョンにアップグレードする | Microsoft Docs"
description: "Configuration Manager を使用して、オペレーティング システムを Windows 7 以降から Windows 10 にアップグレードする方法について説明します。"
ms.custom: na
ms.date: 02/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 1035dbbf944a3a467d637a4a948a75b0946eb711
ms.openlocfilehash: 026d61113a918e43ac4395ef092b1931f33f16d3
ms.contentlocale: ja-jp
ms.lasthandoff: 07/11/2017

---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用して、Windows を最新のバージョンにアップグレードする

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager で、対象のコンピューター上のオペレーティング システムを Windows 7 以降から Windows 10 に、または Windows Server 2012 から Windows Server 2016 にアップグレードするためのステップを説明します。 スタンドアロン メディアやソフトウェア センターなどのさまざまな展開方法の中から選ぶことができます。 一括アップグレード シナリオ:  

-   現在、以下を実行しているコンピューターでオペレーティング システムをアップグレードします。
    - Windows 7、Windows 8、または Windows 8.1。 Windows 10 のビルドからビルドへのアップグレードを実行することもできます。 たとえば、Windows 10 RTM を Windows 10 バージョン 1511 にアップグレードできます。  
    - Windows Server 2012。 Windows Server 2016 のビルドからビルドへのアップグレードを実行することもできます。 サポートされているアップグレード パスの詳細については、[サポートされているアップグレード パス](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016)に関するページを参照してください。    

-   コンピューター上のアプリケーション、設定、ユーザー データは保持されます。  

-   Windows ADK などの外部依存関係はありません。  

-   従来のオペレーティング システム展開よりも高速で、回復力があります。  

 タスク シーケンスを使用してネットワーク経由でオペレーティング システムを展開するには、次のセクションを使用します。  

##  <a name="BKMK_Plan"></a> プラン  

-   **オペレーティング システムをアップグレードするタスク シーケンスの制限を確認する**  

     オペレーティング システムをアップグレードするタスク シーケンスの次の要件と制限を確認して、ニーズに合うかどうかを確かめます。  

    -   オペレーティング システムを展開して、イメージがインストールされてからコンピューターを構成する中心的タスクに関連したタスク シーケンスのステップのみを追加しなければなりません。 これには、パッケージ、アプリケーション、または更新プログラムをインストールするステップと、コマンド ライン、PowerShell、または動的変数の設定を実行するステップが含まれます。  

    -   アップグレード タスク シーケンスを展開する前に、コンピューターにインストールされたドライバーとアプリケーションを確認して、それらが Windows 10 と互換性があることを確かめます。  

    -   次のタスクは一括アップグレードと互換性がないため、従来のオペレーティング システムの展開を使用する必要があります。  

        -   コンピューターのドメイン メンバーシップを変更するか、ローカル管理者を更新します。  

        -   ディスク パーティション分割や、x86 から x64 へのアーキテクチャの変更、UEFI の実装、または基本オペレーティング システム言語の変更など、コンピューター上の基本的な変更を実装します。  

        -   カスタム基本イメージの使用、サード パーティ ディスク暗号化の使用、WinPE オフライン操作の採用などのカスタム要件があります。<sup></sup>  

-   **インフラストラクチャの要件の計画と実装**  

     アップグレード シナリオの唯一の前提条件は、オペレーティング システムのアップグレード パッケージとタスク シーケンスに含める他のパッケージのための、利用可能な配布ポイントがあることです。 詳細については、[配布ポイントのインストールと変更に関するトピック](../../core/servers/deploy/configure/install-and-configure-distribution-points.md)を参照してください。

##  <a name="BKMK_Configure"></a> 構成  

1.  **オペレーティング システムのアップグレード パッケージを準備する**  

     Windows 10 アップグレード パッケージには、セットアップ先のコンピューターのオペレーティング システムをアップグレードするのに必要なソース ファイルが含まれています。 このアップグレード パッケージは、アップグレードするクライアントと同じエディション、アーキテクチャ、言語にする必要があります。  詳細については、「[オペレーティング システムのアップグレード パッケージの管理](../get-started/manage-operating-system-upgrade-packages.md)」を参照してください。  

2.  **オペレーティング システムをアップグレードするタスク シーケンスを作成する**  

     「[オペレーティング システムをアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)」の手順に従って、オペレーティング システムのアップグレードを自動化します。  

    > [!IMPORTANT]
    > スタンドアロン メディアを使用するときは、タスク シーケンス メディア ウィザードから使用できるように、ブート イメージをタスク シーケンスに追加する必要があります。

    > [!NOTE]  
    > オペレーティング システムを Windows 10 にアップグレードするタスク シーケンスを作成するには、通常、「[オペレーティング システムをアップグレードするタスク シーケンスの作成](create-a-task-sequence-to-upgrade-an-operating-system.md)」のステップを使用します。 タスク シーケンスには、オペレーティング システムのアップグレードの手順に加えて、エンド ツー エンドのアップグレード プロセスを処理するためのお勧めの追加ステップとグループが含まれます。 しかし、カスタム タスク シーケンスを作成し、[オペレーティング システムのアップグレード](../understand/task-sequence-steps.md#BKMK_UpgradeOS)のタスク シーケンス手順を追加して、オペレーティング システムをアップグレードすることができます。 これは、オペレーティング システムを Windows 10 にアップグレードする場合に必要な唯一の手順です。 この方法を選んだ場合は、オペレーティング システムのアップグレードの手順の後に、[コンピューターの再起動](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)の手順も追加してアップグレードを完了します。 必ず **[現在インストールされている既定のオペレーティング システム]** 設定を使用して、Windows PE ではなく、インストール対象のオペレーティング システムでコンピューターを再起動するようにします。  

##  <a name="BKMK_Deploy"></a> デプロイ  

-   オペレーティング システムを展開するには、次の展開方法のいずれかを使用します。  

    -   [ソフトウェア センターを使用したネットワーク経由での Windows の展開](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

## <a name="monitor"></a>モニター  

-   **タスク シーケンスの展開の監視**  

     オペレーティング システムをアップグレードするために、タスク シーケンスの展開を監視するには、「[オペレーティング システムの展開の監視](monitor-operating-system-deployments.md)」を参照してください。  

