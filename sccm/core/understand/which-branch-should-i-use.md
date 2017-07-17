---
title: "適切なブランチを選択する | Microsoft Docs"
description: "System Center Configuration Manager の使用可能な各ブランチの相違点について説明します。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 26356a80bd8c78d4517253bae73e53d8d8f3a73a
ms.contentlocale: ja-jp
ms.lasthandoff: 06/03/2017


---
# 適切な Configuration Manager のブランチを選択する
<a id="which-branch-of-configuration-manager-should-i-use" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)、(Long-Term Servicing Branch)、(Technical Preview)*


2016 年 10 月以降、System Center Configuration Manager の 3 つのブランチを使用できます。 このトピックは、適切なブランチを選択するのに役立ちます。

> [!TIP]  
> 階層内のすべてのサイトは同じブランチを実行する必要があります。 階層内でサイトがそれぞれ異なるブランチをもつことはサポートされません。

## System Center Configuration Manager の Current Branch
<a id="current-branch-of-system-center-configuration-manager" class="xliff"></a>
これは、実稼働環境で使用するためにライセンスされるブランチで、最新の機能を使用することができます。 System Center Datacenter、System Center Standard、System Center Configuration Manager、またはそれらと同等のサブスクリプション権を保有している場合は、このブランチを使用します。 ソフトウェア アシュアランスとライセンス オプションについては、「[System Center Configuration Manager のライセンスとブランチ](learn-more-editions.md)」をご覧ください。


>  [!TIP]
> Current Branch は、ライセンスを必要としない評価版としてインストールできます。 評価版は 180 日間使用でき、Current Branch のライセンス取得済みエディションへのアップグレードをサポートしています。

Current Branch は年に数回更新され、新機能が追加されます。 更新プログラムの各バージョンは、リリース後 1 年間サポートされます。 その 1 年間の有効期間が切れる前に、最新バージョンの Current Branch に更新する必要があります。 新しいバージョンへの更新プログラムは、コンソール内の更新プログラムとして利用できます。

Current Branch を新しいサイトとしてインストールするか、System Center 2012 Configuration Manager (Service Pack 2 を適用済み) または System Center 2012 R2 Configuration Manager (Service Pack 1 を適用済み) からのアップグレードとしてインストールするには、System Center Configuration Manager の[基準メディア](/sccm/core/servers/manage/updates#baseline-and-update-versions)を使用します。これは、System Center 2016 の付属 DVD として提供されており、また、System Center Configuration Manager のスタンドアロン リリースの一部として利用できます。 このメディアへのアクセス方法は、System Center Configuration Manager のライセンス形態によって異なります。 1702 などの新しい基準バージョンでは、LTSB のインストールはサポートされません。

この基準メディアを使用して、Current Branch の評価版の新しいサイトをインストールすることもできます。 評価版のみをインストールする場合は、[TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) の Web サイトからソフトウェアを入手できます。

>  [!NOTE]
> 新しい Configuration Manager 階層のサイトをインストールするには、基準メディアを使用します。 バージョン 1511 などの基準バージョンをインストール済みの場合は、コンソール内の更新プログラムを使用して、サイトを新しいバージョン (1606 など) に更新します。
>
> コンソール内の更新プログラムを使用して更新されたサイトは、基準メディアを使用してインストールされた新しいサイトと同一になります。
>
> 詳細については、「[System Center Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」をご覧ください。

**Current Branch の機能**
- 新機能を利用できるようにする[コンソール内の更新プログラム](/sccm/core/servers/manage/install-in-console-updates)を受信します。
- 既存の機能にセキュリティと品質に関する修正を適用するコンソール内の更新プログラムを受信します。
- 必要に応じてアウトオブバンドの更新プログラムをサポートします。 「[更新登録ツールの使用](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)」または「[修正プログラム インストーラーの使用](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)」をご覧ください。
- Microsoft Intune や他のクラウド ベースのサービスおよびインフラストラクチャと相互運用できます。
- 他の Configuration Manager インストール環境との間で[データの移行](/sccm/core/migration/migrate-data-between-hierarchies)をサポートします。
- 以前のバージョンの Configuration Manager からのアップグレードをサポートします。
- 評価版としてのインストールをサポートしており、後でフル ライセンスのインストールにアップグレードすることができます。

Current Branch の初期リリースは、バージョン 1511 でした。 以降の更新プログラムには、バージョン 1602 や 1606 などがあります。 各バージョンのサポート期間は 1 年間であるため、最新バージョンがリリースされたら、すぐにそのリリースに更新することをお勧めします。 新しいバージョンに更新するまで最大 1 年間待つことができるので、ある更新プログラムをスキップして、後から利用可能な最新バージョンをインストールすることもできます。 各バージョンは累積的な内容となっており、ある更新プログラムをスキップしてから最新バージョンをインストールしても、以前のバージョン以降に追加されたすべての機能と改善点を利用できます。

詳細については、「[Current Branch バージョンのサポート](/sccm/core/servers/manage/current-branch-versions-supported)」をご覧ください。

**更新のオプション**
- 有効なソフトウェア アシュアランスがある場合、Current Branch バージョンにコンソール内の更新プログラムをインストールできます。  
- Current Branch を Technical Preview に変換するオプションはありません。 Technical Preview は、ライセンスを必要としない個別のインストールです。
- Current Branch を Long-Term Servicing Branch (LTSB) に変換するオプションはありません。 Current Branch をアンインストールしてから、新規インストールとして LTSB をインストールする必要があります。

##  System Center Configuration Manager の Long-Term Servicing Branch
<a id="long-term-servicing-branch-of-system-center-configuration" class="xliff"></a>
これは、実稼働環境で使用するためにライセンスされるブランチで、Current Branch を使用しており Configuration Manager ソフトウェア アシュアランス (SA) またはそれと同等のサブスクリプション権が 2016 年 10 月 1 日以降に失効することに同意した Configuration Manager ユーザーが対象となります。 ソフトウェア アシュアランスとライセンス オプションについては、「[System Center Configuration Manager のライセンスとブランチ](learn-more-editions.md)」をご覧ください。

LTSB はバージョン 1606 に基づいています。 このブランチは、新機能の提供や既存の機能の更新を行うコンソール内の更新プログラムを受信しません。 ただし、重要なセキュリティ修正プログラムは提供されます。 LTSB をインストールするには、バージョン 1606 の [基準メディア](/sccm/core/servers/manage/updates#baseline-and-update-versions) (System Center 2016 または System Center Configuration Manager が収録された DVD として取得) を使用する必要があります。

LTSB を新しいサイトとしてインストールするか、またはサポートされている Configuration Manager 2012 サイトからのアップグレードとしてインストールするには、バージョン 1606 の[基準メディア](/sccm/core/servers/manage/updates#baseline-and-update-versions)を使用します。これは、System Center 2016 または System Center Configuration Manager (Current Branch および Long-Term Servicing Branch 1606) リリースの付属 DVD として提供されます。 基準メディアを使用して、Current Branch のバージョン 1606 を実行する新しいサイトをインストールするか、Long-Term Servicing Branch を実行する新しいサイトをインストールすることができます。

> [!TIP]  
> System Center 2016 の詳細については、[System Center 2016 のドキュメント](https://technet.microsoft.com/system-center-docs/system-center)をご覧ください。 このドキュメントでは、System Center 2016 の入手方法についても説明しています。この製品を入手するには、Microsoft ライセンス契約または同様の権利が必要です。

> ボリューム ランセンス サービス センター (VLSC) で System Center Configuration Manager バージョン 1606 を見つけるには、[VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) の **[Downloads and Keys]\(ダウンロードとキー\)** タブに移動し、"system center config" を検索し、**[System Center Config Mgr (current branch and LTSB)]\(System Center Configuration Manager (現在のブランチと LTSB)\)** を選択します。

> System Center 2016 の評価版は、[TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview) から入手することもできます。

**LTSB の機能**
-    重要なセキュリティ修正プログラムを提供するコンソール内の更新プログラムを受信します。
- Configuration Manager の SA 契約または同等の権利が期限切れになったときにインストール オプションを提供します。
- Configuration Manager の有効な SA 契約または同等の権利を保有している場合は、Current Branch へのアップグレード (変換) をサポートします。

**制限事項**  
LTSB は Current Branch のバージョン 1606 をベースにしており、次の制限があります。
- LTSB は、一般公開 (2016 年 10 月) 後の 10 年間、重要なセキュリティ更新プログラムのサポート対象となり、その後、このブランチのサポートは失効します。 サポート ライフサイクルの詳細については、「[Microsoft ライフサイクル ポリシー](https://support.microsoft.com/en-us/lifecycle)」を参照してください。
- サーバーおよびクライアントのオペレーティング システムと SQL Server バージョンのような関連テクノロジの限定されたセットのリストをサポートしています。 このブランチでサポートされる内容の詳細については、「[Long-Term Servicing Branch でサポートされている構成](supported-configurations-for-ltsb.md)」を参照してください。
- 新しい機能の更新プログラムを受信しません。
- Microsoft Intune サブスクリプションの追加はサポートされません。そのため、以下は使用できません。
  -    ハイブリッド MDM 構成の Intune
 - オンプレミス MDM
-    Windows 10 サービス ダッシュボード、サービス プラン、Windows 10 の Current Branch (CB) および Current Branch for Business (CBB) の使用はサポートされません。
- Windows 10 LTSB および Windows Server の今後のリリースはサポートされません。
-    資産インテリジェンスはサポートされません。
-    クラウドベースの配布ポイントはサポートされません。
-    Exchange Connector としての Exchange Online のサポートはサポートされません。
-    プレリリース機能はサポートされません。



**更新のオプション**
- LTSB インストールは、Current Branch インストールに変換できます。 Current Branch への変換は、LTSB のサポートが終了する前または後にかかわらずサポートされます。

  変換には、Microsoft との有効なソフトウェア アシュアランス契約が必要です。 詳細については、次のリンクを参照してください。
  - [Long-Term Servicing Branch の Current Branch へのアップグレード](convert-to-current-branch.md)
  - [System Center Configuration Manager のライセンスとブランチ](learn-more-editions.md)
  - 「[Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」の「[基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#baseline-and-update-versions)」
- LTSB を Technical Preview に変換するオプションはありません。 Technical Preview は、ライセンスを必要としない個別のインストールです。
-    Current Branch の評価版を LTSB インストールにアップグレードすることはできません。


## System Center Configuration Manager の Technical Preview
<a id="technical-preview-for-system-center-configuration-manager" class="xliff"></a>
Technical Preview はラボ環境で使用するためのものです。この環境で、Configuration Manager 向けに開発されている最新の機能を確認してテストできます。 Technical Preview は実稼働環境ではサポートされないため、ソフトウェア アシュアランス ライセンス契約は必要ありません。

Technical Preview を実行する新しいサイトをインストールするには、最新の [System Center Configuration Manager Technical Preview の基準メディア](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview)を使用します。 Technical Preview をインストールすると、毎月新しいバージョンがコンソール内の更新プログラムとして利用できます。

**Technical Preview の機能**
-  Current Branch の最近の基準バージョンに基づいています。
-  インストールを最新の Technical Preview バージョンに更新するコンソール内の更新プログラムを受信します。
-  開発者がフィードバックを希望する、開発中の新機能が含まれています。
-  Technical Preview ブランチにのみ適用される更新プログラムを受信します。

**制限事項**
-  [サポートは限定的](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview)です (単一のプライマリ サイトと最大 10 クライアントのみをサポートするなど)。  
-  Current Branch または LTSB にアップグレードすることはできません。
-  移行機能を使用して別の Configuration Manager インストールとの間でデータのインポートまたはエクスポートを行うことはサポートされていません。
-  以前のバージョンの Configuration Manager からのアップグレードはサポートされていません。
-  評価版としてのインストールはサポートされていません。

Technical Preview に最初に導入された機能は、多くの場合、以降の更新プログラムで Current Branch に追加されます。 それぞれの新しい Technical Preview バージョンには、以前の Technical Preview の機能が Current Branch に追加された後も、それらの機能が引き続き含まれます。

詳細については、「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」をご覧ください。

**更新のオプション**
-    新しい Technical Preview バージョン向けのコンソール内の更新プログラムをインストールできます。
-    Technical Preview を Current Branch または LTSB に変換するオプションはありません。


## ブランチとバージョンを確認する
<a id="identify-your-branch-and-version" class="xliff"></a>
Configuration Manager サイトのバージョン情報を表示すると、ブランチも確認できます。

**バージョン**   
お使いのサイトのバージョンを確認するには、コンソールの左上にある **[System Center Configuration Manager のバージョン情報]** を選択して、**[サイトのバージョン]** を表示します。 サイトのバージョンの一覧については、[]()をご覧ください。

**ブランチ**  
サイトのブランチ (LTSB または Current Branch) を確認するには、コンソールで **[管理]** > **[サイトの構成]** > **[サイト]** を選択し、**[階層設定]** を開きます。 Current Branch に変換するオプションがあり、選択できる状態の場合、サイトは LTSB バージョンを実行しています。 サイトが Current Branch を実行している場合、このオプションは淡色表示されます。
さまざまなバージョンの Configuration Manager については、[Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)に関するページの「基準バージョンと更新プログラムのバージョン」をご覧ください。

