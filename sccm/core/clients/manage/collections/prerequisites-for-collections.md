---
title: "コレクションの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager でコレクションを使用するための前提条件について説明します。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 81342ab0d064e3f2da19126819bdd048270a4320
ms.contentlocale: ja-jp
ms.lasthandoff: 12/16/2016


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager のコレクションの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のコレクションには、製品内依存関係のみが含まれます。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|レポート サービス ポイント|コレクションに対してレポートを実行するには、事前に レポート サービス ポイント サイト システムの役割がインストールされている必要があります。 詳細については、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」を参照してください。|  
|コレクションを管理するには、特定のセキュリティ アクセス許可が付与されている必要があります|コンプライアンス設定を管理するには、次のセキュリティのアクセス許可が必要です。<br /><br /> - コレクションを作成し、管理する場合: **コレクション** オブジェクトに対する**作成**、**削除**、**変更**、**フォルダーの変更**、**オブジェクトの移動**、**読み取り**、および**リソースの読み取り**のアクセス許可。<br /><br /> - コレクションの設定を管理する場合: **コレクション** オブジェクトに対する**コレクション設定の変更**のアクセス許可。<br /><br /> **フォルダーの変更** のアクセス許可は、ルート フォルダーを含む、すべてのコレクション フォルダーに必要です。|  

