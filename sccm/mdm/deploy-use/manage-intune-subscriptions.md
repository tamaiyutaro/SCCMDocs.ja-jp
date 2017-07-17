---
title: "System Center Configuration Manager に関連付けられた Intune サブスクリプションの管理 | Microsoft Docs"
description: "System Center Configuration Manager に関連付けられた Intune サブスクリプションを管理します。"
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 2cb4d724c8b78657458a30c0bb020f67c6b62795
ms.contentlocale: ja-jp
ms.lasthandoff: 06/03/2017

---
# System Center Configuration Manager に関連付けられた Intune サブスクリプションの管理
<a id="manage-an-intune-subscription-associated-with-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune (試用版サブスクリプションまたは有料サブスクリプション) を Configuration Manager に追加してから、別の Intune サブスクリプションに切り替える必要がある場合は、**Microsoft Intune サブスクリプション**と**サービス接続ポイント**の両方を Configuration Manager コンソールから削除する必要があります。これにより、新しいサブスクリプションを追加することができるようになります。

> [!NOTE]
> ハイブリッド モバイル デバイス管理では 1 回につき 1 つだけ Intune サブスクリプションを構成できます。

## Configuration Manager から Intune サブスクリプションを削除する方法
<a id="how-to-delete-an-intune-subscription-from-configuration-manager" class="xliff"></a>

> [!IMPORTANT]
>  サブスクリプションを削除すると、Intune サブスクリプションによって管理されるデバイスに構成された、ユーザー登録、ポリシー、アプリの展開などのすべてのコンテンツが削除されます。

1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[Cloud Services]** > **[Microsoft Intune サブスクリプション]** の順に移動します。

2.  表示された **[Microsoft Intune サブスクリプション]** を右クリックしてから、**[削除]** をクリックします。

3.   ウィザードで、**[Configuration Manager から Microsoft Intune サブスクリプションを削除]**、**[次へ]**、**[次へ]** の順にクリックして、サブスクリプションを削除します。


## サービス接続ポイントの役割を削除する方法
<a id="how-to-remove-the-service-connection-point-role" class="xliff"></a>

1.  **[管理]** > **[概要]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に移動します。

2.  **[サービス接続ポイント]** の役割をホストするサーバーを選びます。

3.  **[サイト システムの役割]** 一覧で、**[サービス接続ポイント]** を選んでから、リボンに表示されている **[役割の削除]** をクリックします。 ロールを削除することを確認します。 サービス接続ポイントが削除されます。

これで、新しいサービス接続ポイントを作成したり、Configuration Manager に新規 Intune サブスクリプションを追加したり、Configuration Manager を MDM 機関として設定したりできるようになります。

## MDM 機関を Intune に変更する方法
<a id="how-to-change-mdm-authority-to-intune" class="xliff"></a>
Configuration Manager バージョン 1610 および Microsoft Intune バージョン 1705 以降では、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除してから再登録しなくても、MDM 機関を変更することができます。 詳細については、「[MDM 機関を変更する](/sccm/mdm/deploy-use/change-mdm-authority)」を参照してください。

