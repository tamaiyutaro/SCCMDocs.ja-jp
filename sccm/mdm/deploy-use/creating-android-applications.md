---
title: "Android アプリケーションの作成 | Microsoft Docs"
description: "Android デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 344b55aecd72479b759b40e8252e64a06c5eaba0
ms.openlocfilehash: 3bfb7364c3de5264a5fa8a684965d9aebeb84719
ms.contentlocale: ja-jp
ms.lasthandoff: 07/13/2017

---
# System Center Configuration Manager で Android アプリケーションを作成する
<a id="create-android-applications-with-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager アプリケーションには、デバイスにソフトウェアを展開するために必要なインストール ファイルと情報からなる、1 つまたは複数の展開の種類があります。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

 アプリケーションを作成するには、次の 2 通りの方法があります。  

-   アプリケーション インストール ファイルを読み取って、アプリケーションおよび展開の種類を自動的に作成する。  
-   アプリケーションを手動で作成してから、後で展開の種類を追加する。  
-   アプリケーションをファイルからインポートする。  

Configuration Manager アプリケーションと展開の種類の作成に必要な手順については、「[アプリケーションの作成ウィザードを開始する](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)」を参照してください。 また、Android デバイス用アプリケーションを作成して展開するときに、以下の考慮事項について留意してください。  

## Android アプリに関する一般的な考慮事項
<a id="general-considerations-for-android-apps" class="xliff"></a>

Configuration Manager では、Android 用の次のアプリの種類の展開がサポートされています。

|デバイスの種類|サポートされているファイル|
|-|-|
|Android|.apk|

次の展開操作がサポートされています。

|デバイスの種類|サポートされている操作|
|-|-|
|Android|**利用可能**、**必須** インストールとアンインストールの両方に、ユーザーが同意する必要があります。|
|Android for Work | **必須** |

## Android for Work アプリの承認と展開
<a id="approve-and-deploy-android-for-work-apps" class="xliff"></a>
Configuration Manager の管理者は、アプリを承認して [Play for Work Web サイト](https://play.google.com/work)に展開したり、管理対象の Android for Work デバイスにそれらのアプリを展開したりすることもできます。

Play for Work ストアのアプリを承認し、Configuration Manager コンソールと同期し、管理対象の Android for Work デバイスに展開するには、次の手順を実行します。 アプリをユーザーの仕事用プロファイルに展開するには、Play for Work でアプリを承認し、アプリを Configuration Manager コンソールと同期する必要があります。

1. ブラウザーを開き、https://play.google.com/work にアクセスします。
2. Intune テナントにバインドした Google 管理者アカウントを使用してサインインします。
3. 環境に展開するアプリを参照し、各アプリについて **[承認]** を選択して、Android for Work でアプリを使用できるようにします。
4. Configuration Manager コンソールで **[管理者]** > **[概要]** > **[クラウド サービス]** > **[Android for Work]** の順にクリックし、**[同期]** を選択します。
5. アプリが同期されるまで 10 分間待ってから **[ソフトウェア ライブラリ]** > **[概要]** > **[アプリケーション管理]** > **[ストア アプリのライセンス情報]** の順に選択します。
6. Play for Work から同期したアプリを選択してから **[アプリケーションの作成]** をクリックします。
7. ウィザードを終了して、**[閉じる]** を選択します。
8. **[ソフトウェア ライブラリ]** > **[概要]** > **[アプリケーション管理]** > **[アプリケーション]** の順に選択し、Android for Work アプリを選択して、通常どおりに展開します。

Play for Work アプリを Configuration Manager と同期するには、最初に少なくとも 1 つのアプリを Play for Work Web サイトで承認する必要があります。

