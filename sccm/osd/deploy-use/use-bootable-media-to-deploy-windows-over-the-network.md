---
title: "起動可能なメディアを使用したネットワーク経由での Windows の展開 | Microsoft Docs"
description: "System Center Configuration Manager での起動可能なメディアによる展開を使用して、セットアップ先のコンピューターの起動と同時にオペレーティング システムを展開できます。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: mattbriggs
ms.author: mattbriggs
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 9b20e5e2a66d92038033e816e6fc701581c48a7f
ms.contentlocale: ja-jp
ms.lasthandoff: 06/28/2017


---
# System Center Configuration Manager で起動可能なメディアを使用してネットワーク経由で Windows を展開する
<a id="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

起動可能なメディアによる展開を使用してセットアップ先のコンピューターを起動するときにオペレーティング システムを展開できます。 メディアには、タスク シーケンス、オペレーティング システム イメージ、およびその他のネットワーク上の必要なコンテンツへのポインターが含まれています。 セットアップ先コンピューターは、起動するときに、ポインターで参照されている項目を取得します。 コンテンツのない起動可能なメディアを使用すると、メディア上で交換しなくてもセットアップ先コンピューターを更新できます。

次に挙げるオペレーティング システムの展開シナリオでは、マルチキャストを使用してネットワーク経由でオペレーティング システムを展開できます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)  

いずれかのオペレーティング システムの展開シナリオの手順を完了してから、次のセクションを使用して、起動可能なメディアでオペレーティング システムを展開します。  

## 展開の設定の構成
<a id="configure-deployment-settings" class="xliff"></a>  
起動可能なメディアを使用してオペレーティング システムの展開プロセスを開始する場合、オペレーティング システムをメディアから使用できるように展開を構成します。 このオプションはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで設定することができます。 **[利用できるようにする項目]** の設定では、次のいずれかを設定します。

-   Configuration Manager クライアント、メディア、PXE

-   メディアと PXE のみ

-   メディアと PXE のみ (非表示)

## 起動可能なメディアを作成する
<a id="create-the-bootable-media" class="xliff"></a>
起動可能なメディアとして USB フラッシュ ドライブと CD/DVD セットのどちらかを指定できます。 起動可能なドライブに選ぶオプションは、メディアを起動するコンピューターがサポートするものでなければなりません。 詳細については、「[起動可能なメディアの作成](create-bootable-media.md)」を参照してください。  

##  <a name="BKMK_Deploy"></a> 起動可能なメディアからオペレーティング システムをインストールする  
コンピューターの起動可能なドライブに起動可能なメディアを挿入し、電源を入れてオペレーティング システムをインストールします。

