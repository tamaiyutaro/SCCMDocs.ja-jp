---
title: "System Center Configuration Manager と Microsoft Intune を使った iOS および Mac のハイブリッド デバイス管理のセットアップ | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用して iOS デバイス管理を設定します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ed6b65a1a5aabc0970cd0333cb033405cf6d2aea
ms.openlocfilehash: 52596b211acb1182cb38259cba267bdd0846de80
ms.contentlocale: ja-jp
ms.lasthandoff: 07/03/2017


---
# System Center Configuration Manager と Microsoft Intune で iOS ハイブリッド デバイス管理の設定します
<a id="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager と Intune を使用して、iOS および Mac OS デバイスの登録を有効にし、iPhone、iPad、Mac のユーザーが会社の電子メールとリソースにアクセスできるようにします。 ユーザーが Intune の会社のポータル アプリをインストールすると、そのデバイスをポリシーの対象にできます。 iOS および Mac デバイスを管理するには、Apple Push Notification サービス (APNs) 証明書を Apple からインポートする必要があります。 この証明書で、Intune が Apple のデバイス管理サービスと接続を確立して、iOS と Mac デバイスを管理できるようになります。  

 企業所有の iOS デバイスを登録することもできます。  「[Enroll company-owned devices](enroll-company-owned-devices.md)」 (会社所有のデバイスの登録) をご覧ください。  

## iOS デバイス登録の有効化
<a id="enable-ios-device-enrollment" class="xliff"></a>  
 iOS デバイス登録を準備するには、次の手順に従います。  

#### Configuration Manager での iOS デバイス登録のセットアップ
<a id="set-up-ios-device-enrollment-in-configuration-manager" class="xliff"></a>  

1.  **前提条件** - 任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」の前提条件と手順を完了しておく必要があります。    

2.  **証明書署名要求をダウンロード** - Apple からの APNs 証明書を要求するには、証明書署名要求ファイルが必要です。  

    1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** >  **[Microsoft Intune サブスクリプション]** に移動します。  

    2.  **[ホーム]** タブで、 **[APNs 証明書要求の作成]**をクリックします。 **[Apple Push Notification サービス証明書署名要求の要求]** ダイアログ ボックスが開きます。  

    3.  **[参照]** をクリックして、新しい証明書署名要求ファイルの保存先のパスを指定します。 証明書署名要求ファイルをローカルに保存します。  

    4.  **[ダウンロード]**をクリックします。 新しい Microsoft Intune 証明書署名要求ファイルがダウンロードされ、Configuration Manager によって保存されます。 証明書署名要求ファイルは、Apple Push Certificates Portal からの信頼関係証明書を要求するために使用します。  

3.  **Apple からの APNs 証明書の要求** - Apple Push Notification サービス (APNs) 証明書は、管理サービス、Intune、および登録済み iOS モバイル デバイスの間に信頼関係を確立するために使用されます。  

    1.  ブラウザーで [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) に接続し、会社の Apple ID でサインインします。 この Apple ID は、将来 APNs 証明書を更新するときにも使用する必要があります。  

    2.  証明書署名要求 (.csr) ファイルを使用してウィザードを完了します。 APNs 証明書をダウンロードして、pem ファイルをローカルに保存します。 この APNs 証明書 (.pem) ファイルは、Apple Push Notification サーバーと Intune のモバイル デバイス管理機関との間に信頼関係を確立するために使用されます。  

4.  **登録を有効にし、APNs 証明書をアップロード** - iOS の登録を有効にするには、APNs 証明書をアップロードします。  

    1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]**  >  **[Microsoft Intune サブスクリプション]** に移動します。  

    2.  **[ホーム]** タブの **[サブスクリプション]** グループで、**[プラットフォームの構成]**  >  **[iOS]** の順にクリックします。  

        > [!NOTE]  
        >  Configuration Manager コンソールで iOS の登録が有効になるまでは、Apple Push Notification サービス (APNs) 証明書をアップロードしないでください。  

    3.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、 **[iOS]** タブを選択し、 **[iOS の登録を有効にする]** チェック ボックスをオンにします。  

    4.  **[参照]**をクリックし、Apple からダウンロードした APNs 証明書 (.cer) ファイルに移動します。 Configuration Manager に APNs 証明書情報が表示されます。 **[OK]** をクリックして、APNs 証明書を Intune に保存します。  

 セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 「[デバイスの登録についてユーザーに通知する事柄](https://docs.microsoft.com/intune/end-user-educate)」に関する記事をご覧ください。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

> [!div class="button"]
[< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)

