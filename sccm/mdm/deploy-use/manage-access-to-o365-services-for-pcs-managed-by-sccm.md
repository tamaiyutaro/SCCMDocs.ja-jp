---
title: "管理対象 PC の O365 サービスへのアクセスを管理する | Microsoft Docs"
description: "System Center Configuration Manager で管理されている PC の条件付きアクセスを構成する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c8717925dba42451b1e241a7c2f59e43896d7d99
ms.openlocfilehash: e78fe989b7ff445717c8320c4eae3900eb46baea
ms.contentlocale: ja-jp
ms.lasthandoff: 06/19/2017


---
# System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する
<a id="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager のバージョン 1602 より、System Center Configuration Manager によって管理されている PC の条件付きアクセスを構成することができます。  

> [!IMPORTANT]  
> これは、更新プログラム 1602、更新プログラム 1606、更新プログラム 1610 で使用できるプレリリース機能です。 プレリリース機能は、運用環境での早期テストのためにこの製品に含まれていますが、運用環境で使用することはできません。 詳細については、「[更新プログラムからプレリリース機能を使用する](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease)」を参照してください。
> - 更新プログラム 1602 をインストールすると、プレリリース機能であっても機能の種類はリリース済みとして表示されます。
> - その後 1602 から 1606 に更新した場合、プレリリース機能のままですが、機能の種類はリリース済みとして表示されます。
> - バージョン 1511 から 1606 に直接更新した場合、機能の種類はプレリリースとして表示されます。

Intune によって登録および管理されているデバイスへの条件付きアクセスや、ドメインに参加していてコンプライアンス評価対象ではない PC への条件付きアクセスを構成する方法については、「[System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)」を参照してください。

## サポートされているサービス
<a id="supported-services" class="xliff"></a>  

-   Exchange Online
-   SharePoint Online

## サポートされている PC
<a id="supported-pcs" class="xliff"></a>  

-   Windows 7
-   Windows 8.1
-   Windows 10 

## 条件付きアクセスの構成
<a id="configure-conditional-access" class="xliff"></a>  
 条件付きアクセスをセットアップするには、最初にコンプライアンス ポリシーを作成して、条件付きアクセス ポリシーを構成する必要があります。 コンプライアンス ポリシーに対応している PC のみが Exchange Online サービスと SharePoint Online サービスにアクセスできるように、PC の条件付きアクセス ポリシーを構成できます。  

### 必要条件
<a id="prerequisites" class="xliff"></a>  

-   ADFS の同期と O365 サブスクリプション。 O365 サブスクリプションは、Exchange Online と SharePoint Online のセットアップのためのものです。  

-   Microsoft Intune サブスクリプション。 Microsoft Intune サブスクリプションは、Configuration Manager コンソールで構成される必要があります。 Azure Active Directory にデバイスのコンプライアンス対応状態を中継するために、また、ユーザー ライセンスのために、Intune サブスクリプションが使用されます。  

 PC は、次の要件を満たす必要があります。  

-   Azure Active Directory への自動デバイス登録の[前提条件](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)   

     コンプライアンス ポリシーに基づいて Azure AD に PC を登録できます。  

    -   Windows 8.1 と Windows 10 の PC では、Active Directory グループ ポリシーを使用して、Azure AD に自動的に登録するデバイスを構成することができます。  

    -   Windows 7 の PC の場合には、System Center Configuration Manager を利用して Windows 7 PC にデバイス登録ソフトウェア パッケージを展開する必要があります。 詳細については、「[Azure Active Directory への Windows ドメイン参加済みデバイスの自動デバイス登録](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)」トピックを参照してください。  

-   先進認証が [有効になっている](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)Office 2013 または Office 2016 を使用する必要があります。  

 下記の手順は、Exchange Online と SharePoint Online の両方に適用されます。  

### 手順 1. コンプライアンス ポリシーの構成
<a id="step-1-configure-compliance-policy" class="xliff"></a>  
 Configuration Manager コンソールで、次の規則を含むコンプライアンス ポリシーを作成します。  

-   Azure Active Directory への登録が必要: この規則は、ユーザーのデバイスが Azure AD に社内参加しているかどうかをチェックし、参加していない場合には Azure AD に自動的に登録します。 自動登録がサポートされているのは Windows 8.1 のみです。 Windows 7 PC の場合には、MSI を展開して自動登録を実行します。 詳細については、 [Azure Active Directory への自動デバイス登録](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)に関する記事を参照してください。  

-   **必要な更新が特定の日数の期限を過ぎている場合、そのすべてをインストール:** このルールは、ユーザーが指定した期限および猶予期間内の必須のすべての更新 (「Required automatic updates」 (必須の自動更新) ルールで指定) がユーザーのデバイスに含まれているかどうかを確認し、保留されている必須の更新すべてを自動的にインストールします。  

-   **BitLocker ドライブ暗号化が必要:** これは、デバイスのプライマリ ドライブ (C:\\ など) が BitLocker で暗号化されたかどうかをチェックします。 Bitlocker 暗号化がプライマリ デバイスで有効でない場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

-   **マルウェア対策が必要:** これは、マルウェア対策ソフトウェア (System Center Endpoint Protection または Windows Defender 限定) が有効で実行されているかどうかをチェックします。 無効な場合、電子メール サービスおよび SharePoint サービスへのアクセスがブロックされます。  

### 手順 2. 条件付きアクセスの効果の評価
<a id="step-2-evaluate-the-effect-of-conditional-access" class="xliff"></a>  
 条件付きアクセス コンプライアンス レポートを実行します。 このレポートは [レポート] > [コンプライアンスと設定の管理] の [監視] セクションにあります。 これには、すべてのデバイスのコンプライアンス対応状態が表示されます。  非対応としてレポートされたデバイスから Exchange Online および SharePoint Online へのアクセスはブロックされます。  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### Active Directory セキュリティ グループの構成
<a id="configure-active-directory-security-groups" class="xliff"></a>  
 条件付きアクセス ポリシーは、ポリシーの種類に応じてユーザーのグループを対象とします。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 サービスにアクセスするには、ポリシーの対象であるユーザーが使用する各デバイスがポリシーに対応している必要があります。  

 Active Directory セキュリティ ユーザー グループ。 これらのユーザー グループは、Azure Active Directory に同期される必要があります。 これらのグループを Office 365 管理センターまたは Intune アカウント ポータルで構成することもできます。  

 各ポリシーには、次の 2 つのグループの種類を指定できます。 :  

-   **対象グループ** – ポリシーが適用されるユーザー グループ。 コンプライアンスと条件付きアクセス ポリシーの両方に同じグループを使用してください。  

-   **例外グループ** – ポリシーから除外されるユーザー グループ (省略可能)  
    ユーザーが両方に含まれている場合は、ポリシーから除外されます。  

     条件付きアクセス ポリシーの対象となるグループだけが評価されます。  

### 手順 3.  Exchange Online および SharePoint Online の条件付きアクセス ポリシーを作成します。
<a id="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online" class="xliff"></a>  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**をクリックします。  

2.  Exchange Online のポリシーを作成するには、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]**を選びます。  

     SharePoint Online のポリシーを作成するには、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]**を選びます。  

3.  [ **ホーム** ] タブの [ **リンク** ] グループで、[ **Intune コンソールでの条件付きアクセス ポリシーの構成**] をクリックします。 Configuration Manager を Intune に接続するために使用されるアカウントのユーザー名とパスワードを指定する必要がある場合があります。  

     Intune 管理コンソールが開きます。  

4.  Exchange Online の場合は、Microsoft Intune の管理コンソールで **[ポリシー] > [条件付きアクセス] > [Exchange Online ポリシー]** をクリックします。  

     SharePoint Online の場合は、Microsoft Intune の管理コンソールで **[ポリシー] > [条件付きアクセス] > [SharePoint Online ポリシー]** をクリックします。  

5.  Windows PC の要件を**[デバイスは準拠デバイスである必要があります]**オプションに設定します。  

6.  **[対象グループ]**で、 **[変更]** をクリックして、ポリシーを適用する Azure Active Directory セキュリティ グループを選択します。  

    > [!NOTE]  
    >  コンプライアンス ポリシーの展開と条件付きアクセス ポリシーの対象グループに同じセキュリティ ユーザー グループを使用してください。  

     **[例外グループ]**で、必要に応じて **[変更]** をクリックして、このポリシーから除外する Azure Active Directory セキュリティ グループを選択します。  

7.  **[保存]** をクリックしてポリシーを作成および保存します  

 非対応であるためにブロックされているエンドユーザーに対しては、System Center Configuration Manager ソフトウェア センターにコンプライアンス情報が表示されます。コンプライアンスに関する問題が解決されたら、そのようなエンドユーザーが新しいポリシー評価を開始します。  

<!---
##  <a name="bkmk_KnownIssues"></a> Known issues  
 You may see the following issues when using this feature:  

-   In this 1602 update,  the 5 day compliance is not enforced. Even if compliance check on the end-user's device has happened more than 5 days ago, users still can access Office 365 and SharePoint online.  

-   When a device is not compliant with the compliance policy, the reason is not automatically displayed. The end- user must go to the new Software Center to find the reason for non-compliance. The reason is displayed in the Device compliance section of the Software Center.  

-   Windows 10 users may see multiple access failures when trying to reach O365 and/or SharePoint online resources. Note that conditional access is not fully supported for Windows 10.  
--->
## 関連項目
<a id="see-also" class="xliff"></a>

- [System Center Configuration Manager でのデータとサイト インフラストラクチャの保護](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Configuration Manager の条件付きアクセスによるトラブルシューティング フローチャート](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)

