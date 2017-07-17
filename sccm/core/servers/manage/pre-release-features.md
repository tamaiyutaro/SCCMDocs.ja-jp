---
title: "プレリリース機能 | Microsoft Docs"
description: "System Center Configuration Manager のプレリリース機能"
ms.custom: na
ms.date: 6/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 988f8da0b221f8c0b470e7a0a8ed995356193f98
ms.contentlocale: ja-jp
ms.lasthandoff: 06/13/2017


---
# System Center Configuration Manager のプレリリース機能
<a id="pre-release-features-in-system-center-configuration-manager" class="xliff"></a>
*適用対象: System Center Configuration Manager (Current Branch)*

プレリリース機能は、運用環境での初期テスト用の Current Branch に含まれている機能です。 これらの機能は完全にサポートされていますが、現在開発中のため、プレリリースのカテゴリから移動するまでは変更が行われる可能性があります。

 プレリリース機能を使用できるようになる前に、Configuration Manager コンソールのプレリリース機能を使用することに同意してはじめて、その機能を選択して使用を有効にすることができます。  

同意する操作は階層ごとに 1 回限りの操作であり、元に戻すことはできません 同意するまでは、更新プログラムに含まれている新しいプレリリース機能を有効にすることはできません。 プレリリース機能を有効にした後で無効にすることはできません。

同意するには、コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** に移動してから、**[階層設定]** を選択します。 **[全般]** タブで、**[プレリリース機能を使用することに同意する]** を選択します。

 > [!NOTE]
 > 1602 より後の更新バージョンをインストールする前に更新プログラム 1602 のプレリリース機能を有効にした場合は、プレリリース機能を使用することに同意しなくても、それらの機能は有効です。

プレリリース機能を含む更新プログラムをインストールすると、これらの機能は、更新プログラムに含まれる標準の機能と一緒に、[更新とサービス] ウィザードに表示されます。
  - **既に同意した場合:** 更新プログラムのインストール時に、[更新とサービス] ウィザード内でプレリリース機能を有効にすることができます。 これを行うには、その他の機能の場合と同様に、プレリリース機能を選択します。     

    必要に応じて、後でコンソールの **[管理]** > **[更新とサービス]** > **[機能]** ノードからプレリリース機能を有効にすることもできます。 **[機能]** ノードで、機能を選択し、**[有効にする]** を選択します。 このオプションは同意するまで灰色表示のままです  (1702 より前のバージョンでは、[更新とサービス] は、**[管理]** > **[クラウド サービス]** にありました)。
  -   **まだ同意していない場合:** 更新プログラムのインストール時に、プレリリース機能は [更新とサービス] ウィザードに表示されますが、灰色表示になっていて、有効にすることはできません。 更新プログラムをインストールしたら、**[機能]** ノードでこれらの機能を表示できます。 ただし、**[階級設定]** で同意するまではこれらの機能を有効にすることはできません。

スタンドアロン プライマリ サイトで同意し、新しい中央管理サイトをインストールして階層を拡張する場合、中央管理サイトでもう一度同意する必要があります。

 プレリリース機能を有効にすると、Configuration Manager の階層マネージャー (HMAN) は機能が利用可能になる前に変更を処理する必要があります。 多くの場合、変更の処理はすぐに行われますが、HMAN の処理サイクルによっては完了までに最大で 30 分かかることがあります。 変更が処理された後、その機能に関連する新しい UI が表示されるようにするには、コンソールを再起動する必要があります。

**利用できるプレリリース機能:**

 |機能          |プレリリース版として追加 | 完全機能として追加|  
|------------------|---------------------|---------------------|
| Configuration Manager を使用した Device Guard 管理 |  [バージョン 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| アプリケーションをインストールする前に実行中の実行可能ファイルを確認する  |   [バージョン 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| データ ウェアハウス サービス ポイント  |  [バージョン 1702](/sccm/core/servers/manage/data-warehouse) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クライアントへのコンテンツ配布のピア キャッシュ |  [バージョン 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クラウド管理ゲートウェイ |  [バージョン 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クライアント データ ソース ダッシュボード |  [バージョン 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite コネクタ  | [バージョン 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| クラスター対応のコレクションのサービス (サーバー グループの提供)| [バージョン 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![未追加](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|System Center Configuration Manager が管理する PC の条件付きアクセス | [バージョン 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [バージョン 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

