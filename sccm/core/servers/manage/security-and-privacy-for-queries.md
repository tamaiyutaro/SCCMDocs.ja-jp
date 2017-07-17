---
title: "クエリのセキュリティとプライバシー | Microsoft Docs"
description: "サイト データベースから情報のクエリを実行するときのセキュリティとプライバシーのベスト プラクティスを理解します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2087badc9dd1d216352dce232b145a786783ac89
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.contentlocale: ja-jp
ms.lasthandoff: 05/18/2017


---
# System Center Configuration Manager のクエリのセキュリティとプライバシー
<a id="security-and-privacy-for-queries-in-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でクエリを使用すると、指定した条件に基づいてサイト データベースの情報を取得できます。 Configuration Manager は、標準操作中にサイト データベース情報を収集します。 たとえば、探索またはインベントリで収集された情報を使用して、特定の条件に合うデバイスを識別するようにクエリを構成することができます。  

 クエリの詳細については、「[System Center Configuration Manager のクエリの概要](../../../core/servers/manage/introduction-to-queries.md)」を参照してください。 クエリを使用して取得できる情報を収集する Configuration Manager 操作に関するセキュリティのベスト プラクティスとプライバシー情報の詳細については、「[System Center Configuration Manager のセキュリティとプライバシー](../../../core/plan-design/security/security-and-privacy.md)」を参照してください。  

## クエリについて推奨するセキュリティ運用方法
<a id="security-best-practices-for-queries" class="xliff"></a>  
 以下は、クエリについてのセキュリティのベスト プラクティスです。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|ネットワークの場所に保存されているクエリをエクスポートまたはインポートする場合は、場所とネットワーク チャネルをセキュリティで保護します。|ネットワーク フォルダーにアクセスできるユーザーを制限します。<br /><br /> ネットワークの場所とサイト サーバーの間で、サーバー メッセージ ブロック (SMB) 署名またはインターネット プロトコル セキュリティ (IPsec) を使用して、攻撃者によってインポートされる前のクエリ データが改ざんされるのを防止します。|  

## 関連項目
<a id="see-also" class="xliff"></a>  
 [System Center Configuration Manager のクエリのテクニカル リファレンス](../../../core/servers/manage/queries-technical-reference.md)

