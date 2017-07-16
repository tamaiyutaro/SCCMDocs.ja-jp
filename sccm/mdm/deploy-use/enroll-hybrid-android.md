---
title: "System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Android デバイス管理のセットアップ | Microsoft Docs"
description: "Configuration Manager と Intune を使用して Android モバイル デバイスを管理できるように準備します。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 86620254897aa9a775dc433de7010b5814c1ec3e
ms.openlocfilehash: af6fa2dfae5549e89c46d05d0cef1e24342558f9
ms.contentlocale: ja-jp
ms.lasthandoff: 07/06/2017


---
# System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Android モバイル デバイスのセットアップ
<a id="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックは、IT 管理者が Android および Android for Work デバイスのハイブリッド登録を有効にする場合に役立ちます。 IT 管理者は、System Center Configuration Manger を使用して、構成された Microsoft Intune サブスクリプションからデバイスを管理できるようになります。 ユーザーは、Google Play から Android 用の会社のポータル アプリをダウンロードすることで、Android (Samsung KNOX Standard を含む) および Android for Work デバイスを登録することができます。

Configuration Manager の管理者は、コンプライアンス設定の管理、Android デバイスのワイプまたは削除、アプリの展開、およびソフトウェアとハードウェアのインベントリの収集を実行できます。 Android 用の会社のポータル アプリを Android デバイスにインストールしなければ、インベントリとコンプライアンス設定などの管理機能を利用できませんが、Android デバイスにアプリを展開することはできます。  

## Android の登録を有効にする
<a id="enable-android-enrollment" class="xliff"></a>  
次の手順で、Configuration Manager が仕事用プロファイルを使用せずに Android デバイスを管理できるようになります (つまり "従来の Android" の登録)。

1. 任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」に記載されている前提条件と手順を完了しておきます。  
2. Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Intune サブスクリプションを選択します。  
3. **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[Android]** の順に選択します。  
4. **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、**[Android]** タブを選択し、**[Android の登録を有効にする]** ボックスをクリックします。  

 セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

## Android for Work の登録を有効にする
<a id="enable-android-for-work-enrollment" class="xliff"></a>
次の手順で、Configuration Manager が仕事用プロファイルを使って、Android デバイスを管理できるようになります。

1. Android for Work の管理者アカウントとして使用する Google アカウントを https://accounts.google.com/SignUp で作成します。 または、この Intune テナントのすべての Android for Work 管理タスクに関連付けられているアカウントでサインインします。 このアカウントは、Android デバイスを管理する管理者間で共有する Google アカウントにすることができます。 これは、組織が Play for Work コンソールでアプリを管理および発行するときに使用する Google アカウントです。 このアカウントを使用して、Play for Work ストアのアプリを承認し、アカウント名とパスワードを追跡します。
2. Android の登録を有効にするには、Google アカウントを Configuration Manager で管理される Intune テナントにバインドします。
   1. Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Intune サブスクリプションを選択します。
   2. **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[Android for Work]** の順に選択します。
   3. ダイアログ ボックスの **[Intune コンソールで Android for Work を構成する]** を選択します。 Web ブラウザーで Intune コンソールが開きます。
   4. Intune 管理者の資格情報を使用して Intune ポータルにサインインします。
   5. **[構成]** を選択して Google Play の Android for Work Web サイトを開きます。
   6. Google のサインイン コンポーネントで、手順 1 の Google アカウントの資格情報を入力し、会社情報を入力します。
3. Intune ポータルに戻ると、Android for Work が有効になり、Android for Work デバイスの 3 つの登録オプションが表示されます。
   - **すべてのデバイスを Android として管理する** (無効)。 Android for Work をサポートするデバイスを含め、すべての Android デバイスが従来の Android デバイスとして登録されます。
   - **サポートされているデバイスを Android for Work として管理する** (有効)。 Android for Work をサポートするすべてのデバイスが Android for Work デバイスとして登録されます。 Android for Work をサポートしない Android デバイスは、従来の Android デバイスとして登録されます。
   - **これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する** (一部のグループのみで有効)。 Android for Work の管理対象を一部のユーザーのみに制限できます。 Android for Work をサポートするデバイスを、選択されたグループのメンバーが登録した場合にのみ、Android for Work デバイスとして登録されます。 それ以外のデバイスは Android デバイスとして登録されます。

> [!NOTE]
> ある既知の問題では、**[これらのグループに所属するユーザーのサポートされているデバイスのみを Android for Work として管理する]** オプションが期待どおり動作しません。 指定の Azure AD グループにあるユーザーのデバイスが、Android for Work ではなく Android として登録されます。 Android for Work を有効にするには、**[Manage all supported devices as Android for Work (サポートされているすべてのデバイスを Android for Work として管理する)]** オプションを利用する必要があります。


セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

バインドが完了すると、アカウント名と組織名が Intune ポータルに表示されます。 その時点で、両方のブラウザーを閉じることができます。

### Android for Work デバイスを登録する
<a id="enroll-an-android-for-work-device" class="xliff"></a>
ユーザーが Android for Work デバイスを登録する方法は、Android の登録方法と似ています。 ユーザーはモバイル デバイスで Android 用の会社のポータル アプリをダウンロードしてインストールできます。 アプリでは登録プロセスの一環で仕事用プロファイルを作成するように求められます。 仕事用プロファイルを作成したら、管理対象バージョンのポータル サイトに切り替える必要があります。 管理対象のポータル サイトには、右下に小さなオレンジ色のブリーフケースのタグが付いています。

### Android for Work デバイスを登録する
<a id="manage-android-for-work-devices" class="xliff"></a>
Android for Work の登録を有効にすると、Android for Work デバイスの次の管理タスクを実行できるようになります。
- [アプリの承認](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [構成アイテムの作成](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [コンプライアンス設定を管理する](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [電子メール プロファイルの管理](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [仕事用プロファイルの選択的ワイプ](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)

