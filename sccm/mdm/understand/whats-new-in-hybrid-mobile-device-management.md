---
title: "ハイブリッド MDM と Configuration Manager の最新情報 | Microsoft Docs"
description: "Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理の新機能について説明します。"
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 1035dbbf944a3a467d637a4a948a75b0946eb711
ms.openlocfilehash: a9e03d4c5b290886bda87fae41e4df362eca1b71
ms.contentlocale: ja-jp
ms.lasthandoff: 07/11/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用したハイブリッド モバイル デバイス管理の新機能

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、System Center Configuration Manager と Intune のハイブリッド展開で使用できるモバイル デバイス管理 (MDM) の新機能の詳細について説明します。  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager のバージョンとの互換性  

 この記事の各セクションでは、3 つの異なるカテゴリにあるハイブリッド機能を一覧表示します。 次のガイダンスを使用すると、各カテゴリの機能とさまざまなバージョンの Configuration Manager との互換性を判断できます。  

|機能のカテゴリ|説明|
|-|-|
|**Microsoft Intune の新機能** | 通常、このカテゴリに一覧表示されたすべての機能は、System Center 2012 R2 Configuration Manager リリースを含むすべての Configuration Manager のリリースで動作します。これらの機能は Intune サービスのみを必要とし、Configuration Manager の追加機能は必要ないためです。|
|**Configuration Manager Technical Preview の新機能**| このカテゴリに一覧表示されたすべての機能は、指定されたバージョンの Technical Preview リリースでのみ動作します。 これらの機能を試すには、機能の説明で指定されたバージョンの Technical Preview をインストールする必要があります。 詳細については、「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」をご覧ください。|
|**Configuration Manager (現在のブランチ) の新機能**| このカテゴリに一覧表示されたすべての機能は、バージョン 1511 や 1602 など、指定されたバージョンの Configuration Manager (現在のブランチ) でのみ動作します。 ハイブリッド展開に旧バージョンの Configuration Manager を使用している場合は、機能の説明で指定されたバージョンの Configuration Manager (現在の分岐) にアップグレードする必要があります。 詳細については、「[System Center Configuration Manager へのアップグレード](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。|

## <a name="july-2017"></a>2017 年 7 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android でサポートされるバージョンに関する通知の追加**

    Android でサポートされるバージョンに関する新しい通知が追加されました。 詳細については、「[Android 4.3 以前のサポートの終了](#notices)」を参照してください。

## <a name="june-2017"></a>2017 年 6 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **MDM 機関を変更する**

  Configuration Manager バージョン 1610 および Microsoft Intune バージョン 1705 以降では、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除してから再登録しなくても、MDM 機関を変更することができます。 詳細については、「[MDM 機関を変更する]( /sccm/mdm/deploy-use/change-mdm-authority)」を参照してください。

- **管理対象ブラウザーとアプリケーション プロキシの統合**

  Intune Managed Browser は、ユーザーがリモートで作業している場合でも内部の Web サイトにアクセスできるように、Azure AD アプリケーション プロキシ サービスに統合できるようになりました。 ブラウザーのユーザーが、通常と同じようにサイトの URL を入力すると、Managed Browser がアプリケーション プロキシの Web ゲートウェイを介して要求をルーティングします。 詳細については、「[Managed Browser ポリシーを使用したインターネット アクセスの管理](/intune/app-configuration-managed-browser)」を参照してください。

- **Android 用ポータル サイト アプリのアプリの保護ポリシーのエンド ユーザー エクスペリエンスが新しくなりました**

  お客様のフィードバックに基づいて、Android 用ポータル サイト アプリを変更し、**[会社のコンテンツにアクセスする]** ボタンを表示しました。 目的は、エンド ユーザーがアプリの保護ポリシーをサポートするアプリで、Intune モバイル アプリケーション管理の機能にのみアクセスする必要があるときに、不要な登録プロセスを経由せずに済むようにすることです。 これらの変更は、[アプリ UI の新機能](/intune/whats-new-app-ui)ページで確認できます。

- **ポータル サイトを簡単に削除するための新しいメニュー操作**

  ユーザーからのフィードバックに基づき、Android 用ポータル サイト アプリで、デバイスからのポータル サイトの削除を開始する新しいメニュー操作を追加しました。 この操作は、ユーザーがデバイスからアプリを削除できるように、Intune の管理からデバイスを削除します。 これらの変更は、[アプリ UI の新機能](/intune/whats-new-app-ui)ページおよび [Android エンドユーザー文書](/intune-user-help/unenroll-your-device-from-intune-android)で確認できます。

- **アプリを Windows 10 Creators Update と同期するための機能強化**

  Windows 10 用のポータル サイト アプリが、Windows 10 Creators Update (バージョン 1703) が搭載されたデバイスのアプリ インストール要求の同期を自動的に開始するようになりました。 これにより、"同期保留中" 状態のときにアプリのインストールが停止する問題が減少します。 また、ユーザーは、アプリ内からの同期を手動で開始することができます。 これらの変更は、[アプリ UI の新機能](/intune/whats-new-app-ui)ページで確認できます。

- **Windows 10 ポータル サイトの新しいガイド機能** 

  Windows 10 用のポータル サイト アプリでは、特定されていないデバイスや登録されていないデバイス向けのガイド付き Intune チュートリアルを利用できるようになります。 新しい機能では、Azure Active Directory の登録 (条件付きアクセス機能に必要) と MDM の登録 (デバイス管理機能に必要) をユーザーに紹介する手順を表示します。 このガイド付きの機能は、ポータル サイトのホーム ページからアクセス可能になります。 ユーザーは、これらの登録を完了していない場合でも引き続きアプリを使用できますが、機能が制限されます。

  この更新プログラムは、Windows 10 Anniversary Update (ビルド 1607) 以上を実行しているデバイスに表示されます。 これらの変更は、[アプリ UI の新機能](/intune/whats-new-app-ui)ページで確認できます。

- **IOS 用ポータル サイト アプリでアプリのタイルの機能強化**

  ポータル サイトで設定したブランドの色を反映するように、ホームページ上のアプリのタイルのデザインを更新しました。 詳細については、[アプリ UI の新機能](/intune/whats-new-app-ui)を参照してください。

- **IOS 用ポータル サイト アプリでアカウントの選択機能を使用できるようになりました**

  IOS デバイスのユーザーは、職場または学校のアカウントを使用して他の Microsoft アプリにサインインしている場合に、ポータル サイトにサインインしたときに新しいアカウントの選択機能が表示されることがあります。 詳細については、[アプリ UI の新機能](/intune/whats-new-app-ui)を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Configuration Manager Technical Preview 1706 の新機能

- **新しいモバイル アプリケーション管理ポリシーの設定**    

  次のモバイル アプリケーション管理 (MAM) ポリシーの設定を使用できるようになりました。

  - **画面キャプチャの禁止 (Android デバイスのみ):** このアプリを使用するときに、デバイスの画面キャプチャ機能をブロックするように指定します。
  - **連絡先の同期を無効にする:** アプリでデバイス上のネイティブ連絡先アプリにデータを保存できなくなります。
  - **印刷を無効にする:** アプリで職場または学校のデータを印刷できなくなります。

  「[Configuration Manager のモバイル アプリケーション管理ポリシーを使ったアプリの保護](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies)」を参照し、新しいアプリの保護のポリシー設定を試してください。

- **新しい Windows 構成アイテムの設定**<!-- 1354715 -->    

  新しい Windows 構成アイテムは、パスワード、デバイス、ストア、および Microsoft Edge の設定のカテゴリで使用できます。 詳細については、「[New Windows configuration item settings](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings)」(新しい Windows 構成アイテム) を参照してください。

- **新しいデバイス コンプライアンス ポリシー ルール**    

  以前は Intune スタンドアロンにのみ使用可能だったコンプライアンス ポリシー用の新しいオプションを構成できるようになりました。 詳細については、「[デバイス コンプライアンス ポリシーの改善](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules)」を参照してください。

- **Android および iOS の登録制限**<!-- 1290826 -->      

  管理者は、ユーザーが、ハイブリッド環境で個人の Android または iOS デバイスを登録できないことを指定できるようになりました。 これにより、宣言済みのデバイス、会社が所有しているデバイス、またはデバイス登録プログラムで登録されている iOS デバイスに登録されるデバイスを制限することができます。 詳細については、「[Android および iOS の登録制限](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions)」を参照してください。

- **Entrust 証明機関のサポート**<!-- 1350740 -->     

  Configuration Manager は Entrust 証明機関をサポートするようになりました。これにより、Microsoft Intune に登録されたデバイスに PFX 証明書を発行できます。    

  Configuration Manager で証明書登録ポイントの役割を追加するときに、証明機関として Entrust を構成できます。 PFX 証明書を発行する新しい証明書プロファイルを追加する場合は、Microsoft または Entrust のいずれかの証明機関を選択できます。

  **既知の問題**: 1706 Technical Preview では、PFX 証明書は、Microsoft 証明機関用に発行されません。 これは、インポートされた PFX 証明書または SCEP プロファイルには影響ありません。

- **macOS VPN プロファイルの Cisco (IPsec) のサポート**  <!-- 1321367 -->    

  接続タイプとして Cisco (IPsec) を指定して macOS VPN プロファイルを作成できます。 詳細については、「[VPN プロファイルの作成](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles)」を参照してください。


## <a name="april-2017"></a>2017 年 4 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **管理対象ブラウザーで利用できる MyApps**

  Microsoft MyApps では、管理対象ブラウザー内のサポートが改善されました。 管理対象ではない管理対象ブラウザーのユーザーは MyApps サービスに直接移動します。そこで管理者によってプロビジョニングされた自分の SaaS アプリにアクセスできます。 Intune 管理の対象になっているユーザーは、組み込まれている管理対象ブラウザーのブックマークから MyApps に引き続きアクセスできます。

- **管理対象ブラウザーとポータル サイトの新しいアイコン**

  管理対象ブラウザーは、Android 版アプリと iOS 版アプリの両方で更新されたアイコンを受け取ります。 新しいアイコンには更新された Intune バッジが含まれ、Enterprise Mobility + Security (EM+S) の他のアプリとの一貫性が向上します。 管理対象ブラウザーの新しいアイコンは、[Intune アプリ UI の新機能に関するページ](/intune/whats-new/whats-new-in-intune-app-ui.md)で確認できます。

  ポータル サイトは、Android 版アプリ、iOS 版アプリ、Windows 版アプリの更新されたアイコンを受け取り、EM+S の他のアプリとの一貫性を向上させます。 アイコンは 4 月から 5 月後半にかけてすべてのプラットフォームに徐々に提供されます。

- **Android ポータル サイトのサインイン進捗状況インジケーター**

  Android ポータル サイト アプリの更新プログラムには、ユーザーがアプリを起動または再開したとき、サインイン進捗状況インジケーターが表示されます。 このインジケーターには新しい状態が次々と表示されます。"接続しています..." から始まり、"サインインしています..." に進み、さらに "セキュリティ要件を確認しています..." に進み、その後、ユーザーはアプリにアクセスできます。 Android のポータル サイト アプリの新しい画面は [Intune アプリ UI の新機能に関するページ](/intune/whats-new/whats-new-in-intune-app-ui.md)で確認できます。

- **アプリが SharePoint Online にアクセスすることを禁止する**

  アプリ基準の条件付きアクセス ポリシーを作成し、アプリ保護ポリシーが適用されていないアプリが [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online) にアクセスすることを禁止できるようになりました。 アプリ基準の条件付きアクセス シナリオでは、Azure ポータルを利用して SharePoint Online へのアクセスを与えるアプリを指定できます。

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Configuration Manager Technical Preview 1704 の新機能

- **アプリ構成ポリシーを使用した Android アプリの構成**

  System Center Configuration Manager (Configuration Manager) のアプリ構成ポリシーを使用して、ユーザーが Android for Work デバイス上でアプリを実行するときに事前に構成された設定を配布できます。 Android アプリ構成ポリシーは、Android for Work が動作しているデバイス上でのみ使用でき、Play for Work ストアの承認済みアプリに適用されます。 この機能を試用する方法については、「[アプリ構成ポリシーを使用した Android アプリの構成](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies)」をご覧ください。

## <a name="march-2017"></a>2017 年 3 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android 用ポータル サイト アプリに関する新しいユーザー エクスペリエンス**

  Android のポータル サイト アプリのユーザー インターフェイスが変わり、より現代的な外観になりました。 注目の新機能:

  - 色: ポータル サイトのタブ ヘッダーに IT が設定したブランディングの色が付きます。
  - アプリ: **[アプリ]** タブの **[おすすめアプリ]** ボタンと **[すべてのアプリ]** ボタンが更新されました。
  - 検索: **[アプリ]** タブの **[検索]** ボタンはフローティング アクション ボタンです。
  - アプリ ナビゲーション: **[すべてのアプリ]** ビューで **[おすすめ]**、**[すべて]**、**[カテゴリ]** のタブ付きビューが表示され、移動がより簡単になりました。
  - サポート: **[マイ デバイス]** タブと **[IT に連絡]** タブが更新され、読みやすくなりました。

  以上の変更に関する詳細については、「[Intune とエンド ユーザー アプリの UI の更新](/intune/whats-new/whats-new-in-intune-app-ui)」を参照してください。

- **Windows 10 ポータル サイトの署名スクリプト**

  Windows 10 ポータル サイト アプリをダウンロードし、サイドロードする必要がある場合に、スクリプトを利用し、組織のアプリ署名プロセスを簡素化および合理化できるようになりました。  スクリプトとその使用方法に関する手順をダウンロードする方法については、TechNet ギャラリーの「[Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript)」 (Windows 10 ポータル サイトの Microsoft Intune の署名スクリプト) を参照してください。 この告知の詳細については、Intune サポート チーム ブログの「[Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/)」 (Windows 10 ポータル サイト アプリを更新する) を参照してください。

- **中国の Android ユーザー向けサポートを強化**

  中国には Google Play ストアがないため、Android デバイスでは中国のマーケットプレースからアプリを入手する必要があります。 ポータル サイトはこのワークフローをサポートします。中国の Android ユーザーをリダイレクトし、現地のアプリ ストアからポータル サイト アプリや Outlook アプリをダウンロードできるようにします。 これにより、モバイル デバイス管理とモバイル アプリケーション管理の両方で、条件付きアクセス ポリシーを有効にしたときのユーザー エクスペリエンスが向上します。 Android 向けのポータル サイト アプリまたは Outlook アプリは中国の次のアプリ ストアで入手できます。

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **ポータル サイト アプリを最新の状態に維持**

  2016 年 12 月に公開した更新プログラムでは、iOS、Android、Windows 8.1 以降、Windows Phone 8.1 以降のデバイスを登録するときに、ユーザーのグループに対する多要素認証 (MFA) の強制を有効にできるようになりました。 この機能は、Android (v5.0.3419.0 以降) 向けまたは iOS (v2.1.17 以降) 向けのポータル サイト アプリの特定のベースライン バージョンがないと動作しません。

  Intune の管理機能は継続的に改善されており、その多くが、サポートされているすべてのプラットフォームのポータル サイト アプリに合わせて、更新プログラムが調整されています。 その結果、機能強化された Intune を最大限に活かし、最高のユーザー エクスペリエンスが得るために、デバイスにインストールされているポータル サイト アプリを最新版に更新することを推奨しています。

  >[!Tip]
  > アプリ ストアからアプリを自動的に更新するようにデバイスを設定するよう、ユーザーに連絡してください。 Android 向けポータル サイト アプリをネットワーク共有で利用できるようにしている場合、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=49140)から最新版をダウンロードできます。

- **iOS および Android の MAM での Microsoft Teams の有効化**

  iOS と Android 向けの Microsoft Teams アプリが Intune モバイル アプリ管理 (MAM) 機能で有効になりました。会話や会社のデータは常に保護された状態で、デバイスを問わず、自由に働く能力をチームに与えることができるようになりました。 詳細については、Enterprise Mobility and Security ブログの「[Microsoft Teams announcement](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/)」 (Microsoft Teams からの告知) を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Configuration Manager Technical Preview 1703 の新機能

- **Apple Volume Purchase Program シナリオのサポートの追加**

   テクニカル プレビュー 1703 以降、次のボリューム購入プログラム (VPP) シナリオがサポートされています。

   - デバイスのライセンス - デバイスのライセンスをサポートし、デバイス コレクションに展開されるアプリで必要なライセンスは、デバイスごとに 1 つのみになりました。  以前は、デバイスのユーザーごとにライセンスを使用する必要がありました。 詳細については、「[ボリューム購入した iOS アプリをデバイス コレクションに展開する](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections)」を参照してください。
   - 1 つのハイブリッド テナントに対する複数の VPP トークンの使用。両方のトークンは VPP アプリを管理するために使用されます。
   - VPP 教育用トークンの使用。ビジネス用トークンと教育用トークンを区別できます。

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager (現在のブランチ) の新機能

Configuration Manager Technical Preview リリースで以前に提供されていた次の機能は、Intune と Configuration Manager (Current Branch) バージョン 1702 のハイブリッド展開で使用できるようになりました。

- [Android for Work のサポート](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [非準拠アプリのコンプライアンス設定](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [PFX 証明書の作成と配布および S/MIME のサポート](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

次の追加のハイブリッド機能も、Configuration Manager (Current Branch) のバージョン 1702 に含まれます。

- **Apple Volume Purchase Program (VPP) のサポートの向上**

  - ライセンスされたアプリをユーザーだけでなくデバイスにも展開できるようになりました。 デバイス ライセンスをサポートするアプリ機能に応じて、次のように、展開時に適切なライセンスが要求されます。

    | Configuration Manager バージョン | アプリでのデバイス ライセンスのサポート | 展開コレクションの種類 | 要求されるライセンス |
    |-|-|-|-|
    |1702 より前|○|ユーザー|ユーザー ライセンス|
    |1702 より前|×|ユーザー|ユーザー ライセンス|
    |1702 より前|○|デバイス|ユーザー ライセンス|
    |1702 より前|×|デバイス|ユーザー ライセンス|
    |1702 以降|○|ユーザー|ユーザー ライセンス|
    |1702 以降|×|ユーザー|ユーザー ライセンス|
    |1702 以降|○|デバイス|デバイス ライセンス|
    |1702 以降|×|デバイス|ユーザー ライセンス|

  - iOS Volume Purchase Program for Education から購入したアプリを展開し追跡できるようになりました。

  - 複数の Apple Volume Purchase Program トークンを Configuration Manager に関連付けることができるようになりました。

  ボリューム購入した iOS アプリの詳細については、[「ボリューム購入 iOS アプリの管理」](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps) を参照してください。

- **ビジネス向け Windows ストアでの基幹業務アプリのサポート**

  ビジネス向け Windows ストアから、カスタマイズされた基幹業務アプリを同期できるようになりました。

- **新しい Mobile Threat Defense 監視ツール**

    Mobile Threat Defense サービス プロバイダーでコンプライアンス状態を監視する新しい方法を利用できるようになりました。

    詳細については、[「Mobile Threat Defense コンプライアンスの監視」](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance) を参照してください。

## <a name="february-2017"></a>2017 年 2 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **ポータル Web サイトのモダナイズ**

  ポータル Web サイトでは、管理対象デバイスを持っていないユーザーを対象とするアプリがサポートされます。 Web サイトは、新しい濃い色の配色、動的な図、ヘルプデスクの連絡先詳細や既存の管理対象デバイスに関する情報を含む "ハンバーガー メニュー" を使用して、他の Microsoft 製品やサービスに合わせられます。 ランディング ページは、おすすめアプリや最近更新されたアプリのカルーセルを使用して、ユーザーが利用できるアプリを強調するために再配置されます。 [[UI の更新]](/intune/whats-new/whats-new-in-intune-app-ui) ページでは、更新前と後のイメージを利用できます。

- **Windows デバイス用の新しい MDM サーバー アドレス**

  Windows および Windows Phone デバイスを登録するための MDM サーバー アドレスは、manage.microsoft.com から enrollment.manage.microsoft.com に変更されました。 Windows または Windows Phone デバイスを登録するときに求められた場合は、MDM サーバー アドレスとして enrollment.manage.microsoft.com を使用するようユーザーに通知してください。 この更新では、EnterpriseEnrollment.contoso.com を manage.microsoft.com にリダイレクトする DNS 内の CNAME を、EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com にリダイレクトする DNS 内の CNAME に置き換える必要もあります。 この変更にについて詳しくは、http://aka.ms/intuneenrollsvrchange をご覧ください。

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Configuration Manager Technical Preview 1702 の新機能

- **Android for Work のサポート**

  Configuration Manager Technical Preview 1702 を使用するハイブリッド MDM 環境で、Android for Work を使用して Android デバイスを管理できるようになりました。 サポートされている Android デバイスを、Android for Work デバイスとして登録できます。これによりデバイス上に作業プロファイルが作成され、Play for Work で承認されたアプリをそこに展開できます。 これらのデバイスの構成項目、コンプライアンス ポリシー、およびリソース アクセス プロファイルを展開することもできます。 詳細については、[「Android for Work のサポート」](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support) を参照してください。

- **非準拠アプリのコンプライアンス設定**

  コンプライアンス ポリシーで、Android および iOS のアプリの非準拠アプリの規則を作成できるようになりました。 デバイスに指定されたアプリケーションがインストールされている場合、それらは "非準拠" としてマークされ、適用される条件付きアクセス ポリシーに従って、会社のリソースにアクセスできなくなります。 詳細については、[「条件付きアクセス デバイス コンプライアンス ポリシーの改善」](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements) を参照してください。

- **PFX 証明書の作成と配布および S/MIME のサポート**

  PFX 証明書を作成してハイブリッド環境のユーザーに展開できるようになりました。 これらの証明書は、ユーザーが登録したデバイスで S/MIME メールの暗号化と復号化に使用できます。 詳細については、[「S/MIME サポートを含む PFX 証明書を作成する」](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support) を参照してください。

- **追加の iOS 構成設定のサポート**
   
    構成項目の一部として、構成できる 42 個の iOS 設定が追加されました。 これらの設定の大部分 (35 個) は、監視対象の iOS デバイスに対して追加されました。 詳細については、[「iOS デバイスの新しいコンプライアンス設定」](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices) を参照してください。

## <a name="january-2017"></a>2017 年 1 月

### <a name="new-in-microsoft-intune"></a>Microsoft Intune の新機能

- **Android 7.1.1 のサポート**

  Intune では、Android 7.1.1 を完全にサポートし管理できるようになりました。

- **iOS デバイスがアクティブでないか、管理コンソールと通信できない問題を解決する**

  ユーザーのデバイスと Intune との接続が切れた場合、会社のリソースへ再度アクセスできるように、新しいトラブルシューティングの手順を指定できます。 「[Devices are inactive, or the admin console cannot communicate with them](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them)」 (デバイスがアクティブでないか、管理コンソールと通信できない) を参照してください。

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Configuration Manager Technical Preview 1701 の新機能

- **ハイブリッド MDM の作成ウィザードで Android と iOS のバージョン指定が不要に**

  ハイブリッド モバイル デバイス管理 (MDM) の Technical Preview 1701 から、Intune で管理されるデバイスの新しいポリシーとプロファイルを作成する場合に Android および iOS の特定のバージョンを指定する必要がなくなりました。 この変更により、新しい Configuration Manager のリリースまたは拡張機能を必要とせずに、ハイブリッド展開で新しい Android および iOS のバージョンによりすばやくサポートを提供できます。 詳細については、「[作成ウィザードで Android と iOS のバージョン指定が不要に](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)」を参照してください。


## <a name="notices"></a>通知

### <a name="end-of-support-for-android-43-and-lower"></a>Android 4.3 以前のサポートの終了
<!---1171127--->
*2017 年 7 月 6 日*

Android の管理対象アプリとポータル サイト アプリから会社のリソースにアクセスするには、Android 4.4 以降が必要になりました。 10 月 1 日以前に更新されていないデバイスは、ポータル サイトまたはそのアプリにアクセスできなくなります。 登録されたすべてのデバイスが 12 月までにインベントリから強制的に削除されるため、結果的に会社のリソースにアクセスできなくなります。 MDM なしのアプリ保護ポリシーを使用している場合、アプリは更新プログラムを受信せず、時間の経過と共にアプリのエクスペリエンスの質が低下します。


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 および System Center 2012 R2 Configuration Manager (RTM): 2017 年 4 月 10 日に終了するハイブリッド モバイル デバイス管理のサポート
*2017 年 1 月 11 日*

System Center 2012 Configuration Manager SP1 と System Center 2012 R2 Configuration Manager RTM のサポートは 2016 年 7 月 12 日に終了しました。 これに続き、2017 年 4 月 10 日にハイブリッド MDM の Microsoft Intune サービスに接続するこれらのリリースのサポートが終了します。 この日付以降、ハイブリッド MDM はこれらのリリースをもって機能を停止します。 Intune コネクタが Intune サービスに接続できなくなるため、管理対象のデバイスは実質的に非管理対象となります。 アップグレードが実施されるまで、Configuration Manager のデータ (ポリシーとアプリケーションなど) は Intune にフローアップせず、管理対象のデバイスのデータは Configuration Manager にフローダウンしません。

Configuration Manager 2012 SP1 または R2 RTM でハイブリッド展開を実行している場合は、2017 年 4 月 10 日より前に、Configuration Manager (Current Branch) または Configuration Manager 2012 (R2 SP1 または SP2) の最新のサポートされているサービス パックにアップグレードしてサービスの中断を回避することをお勧めします。

その他のリソース:
-   [System Center Configuration Manager (Current Branch) へのアップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [System Center 2012 R2 Configuration Manager SP1 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [System Center 2012 Configuration Manager SP2 へのアップグレードの計画](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Windows Phone 8 ポータル サイトのアップロードの廃止
*2016 年 10 月 25 日*

11 月に Windows 8、Windows Phone 8、および Windows RT に対する Intune サポートが廃止され、Windows Phone 8 ポータル サイトのサポートが終了するので、Configuration Manager コンソールでは、署名済みのポータル サイト アプリをアップロードする機能が廃止されました。  既に登録されている Windows 8、Windows Phone 8、および Windows RT デバイスは引き続きサポートされますが、これらのプラットフォームへの追加デバイスの登録はサポートされていません。


### <a name="see-also"></a>関連項目

- [過去のハイブリッド MDM 機能](whats-new-hybrid-archive.md)
- [System Center 2012 Configuration Manager の MDM 向け新機能](https://technet.microsoft.com/library/mt445560.aspx)

