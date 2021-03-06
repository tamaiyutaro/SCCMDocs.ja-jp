---
title: "デバイス登録マネージャーを使用したデバイスの登録 - Configuration Manager | Microsoft Docs"
description: "System Center Configuration Manager を使用して、会社所有のデバイスをデバイス登録マネージャー アカウントで登録します。"
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
caps.latest.revision: 8
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 7573590763c68a4c97d388be1e64054c318da9cc
ms.openlocfilehash: 8c491636925670732e6af67d8c1c741e4793ef96
ms.contentlocale: ja-jp
ms.lasthandoff: 05/17/2017


---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>デバイス登録マネージャーと Configuration Manager を使用したデバイスの登録

*適用対象: System Center Configuration Manager (Current Branch)*

組織は Intune を使用して、単一のユーザー アカウントで多数のモバイル デバイスを管理することができます。 *デバイス登録マネージャー (DEM)* アカウントは、最大で 1,000 台のデバイスを登録できる特別なユーザー アカウントです。 既存のユーザーを DEM アカウントに追加し、特別な DEM 機能を与えます。 登録される各デバイスは 1 つのライセンスを使用します。 このアカウントで登録したデバイスは、個人用デバイスではなく、ユーザー アフィニティのない共有デバイスとして使用することをお勧めします。  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>デバイス登録マネージャーを使った企業所有のデバイスの登録  
 ストア マネージャーやスーパーバイザーにデバイス登録マネージャーのユーザー アカウントを割り当てると、以下を実行できるようにすることができます。  

-   最大 1,000 台のデバイスを登録して管理する  
-   会社のポータル アプリを使用して会社のアプリをインストールする  
-   会社のデータへのアクセスを構成する  

デバイス登録マネージャー アカウントを使用して管理されるデバイスには、次の制限事項が適用されます。

- ストア マネージャーは、ポータル サイトからデバイスをリセットできません。  
- デバイスの社内参加や Azure Active Directory への参加はできません。 このため、これらのデバイスが条件付きアクセスを使用することを防止できます。
-  デバイス登録マネージャーで管理されているデバイスに会社のアプリを展開するには、会社のポータル アプリを **[必須のインストール]** としてデバイス登録マネージャーのユーザー アカウントに展開します。 その後、デバイス登録マネージャーは、会社のポータル アプリを起動して、その他のアプリをインストールできます。
- パフォーマンス向上のため、会社のポータル アプリにはローカル デバイスのみが表示されます。 その他の DEM デバイスのリモート管理は、Configuration Manager コンソールで管理者のみが実行できます。
- 会社のポータル Web サイトは、デバイス登録マネージャー アカウントでは使用できません。 会社のポータル アプリを使用してください。
- (iOS のみ) DEM を利用して iOS デバイスを登録する場合、Apple Configurator またはデバイス登録プログラム (DEP) を利用してデバイスを登録することはできません。

 **デバイス登録マネージャーのシナリオの例:**   
あるレストランで、接客担当スタッフが販売時点管理に使い、調理担当スタッフがオーダー管理に使うタブレットが必要になりました。 従業員には、会社のデータへのアクセスやユーザーとしてのログオンは必要ありません。 Intune 管理者は、デバイス登録マネージャー アカウントを作成し、そのアカウントを使って会社が所有するデバイスを登録しました。 また、レストランのマネージャーがデバイスの登録と管理を行うことができるように、管理者はデバイス登録マネージャーの資格情報を付与することができます。  

 管理者またはマネージャーは、役割に固有のアプリをレストランのデバイスに展開できます。 さらに、管理者はコンソールでデバイスを選んで、モバイル デバイス管理でインベントリから削除することもできます。  

#### <a name="add-a-device-enrollment-manager"></a>デバイス登録マネージャーの追加  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  **[管理]** ワークスペースで、 **[クラウド サービス]**を展開して **[Microsoft Intune サブスクリプション]**をクリックします。 デバイス登録マネージャーを追加する Microsoft Intune サブスクリプションを選び、**[プロパティ]** をクリックします。  

3.  [Microsoft Intune サブスクリプションのプロパティ] ダイアログ ボックスで、**[デバイス登録マネージャー]** タブをクリックします。  

4.  **[追加と削除]** をクリックします。  

5.  **[デバイス登録マネージャー]** ダイアログで、デバイス登録マネージャーとして追加するユーザーのユーザー名を入力して、**[検索]** をクリックします。 デバイス登録マネージャーとして追加するユーザーを選び、**[追加]** をクリックします。  

6.  デバイス登録マネージャーとなるユーザー アカウントを確認して、**[追加と削除]** をクリックします。  サービスにアクセスするユーザーごとにサブスクリプション ライセンスが必要です。*デバイス登録マネージャー*が Intune 管理者になることはできません。 この機能を使用する前に、ライセンスを追加する必要があるかどうかを確認する必要があります。  

7.  デバイス登録マネージャーでは、Bring Your Own Device (BYOD) シナリオの場合にエンド ユーザーが会社ポータルで実行する際と同じ手順で、モバイル デバイスを登録できるようになります。  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Intune からのデバイス登録マネージャーの削除  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  **[管理]** ワークスペースで、 **[クラウド サービス]**を展開して **[Microsoft Intune サブスクリプション]**をクリックします。 デバイス登録マネージャーを追加する Microsoft Intune サブスクリプションを選び、**[プロパティ]** をクリックします。  

3.  [Microsoft Intune サブスクリプションのプロパティ] ダイアログ ボックスで、**[デバイス登録マネージャー]** タブをクリックします。  

4.  削除するデバイス登録マネージャーを**検索**し、**[削除]** をクリックして、**[OK]** をクリックします。  

 デバイス登録マネージャーを削除していも、登録済みのデバイスに影響はありません。 デバイス登録マネージャーを削除した場合:  

-   登録済みデバイスに影響はありません  

-   登録済みデバイスは引き続き完全に管理されます  

-   削除されたデバイス登録マネージャー アカウントの資格情報は依然正しいので、会社ポータルにログオンしてアプリにアクセスできます  

-   削除されたデバイス登録マネージャー アカウントの資格情報では、デバイスのワイプとインベントリからの削除を実行できません  

-   削除されたデバイス登録マネージャー アカウントと登録済みデバイスの関係は残りますが、追加のデバイスは登録できません

