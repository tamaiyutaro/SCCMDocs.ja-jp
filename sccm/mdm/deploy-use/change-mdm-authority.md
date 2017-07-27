---
title: "MDM 機関を変更する | Microsoft Docs"
description: "MDM 機関を Configuration Manager (ハイブリッド) から Intune スタンドアロンへ、またはその逆に変更する方法について説明します。"
keywords: 
author: dougeby
manager: angrobe
ms.date: 06/02/2017
ms.topic: article
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.translationtype: Human Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: b80fec937b50dca3ab995be281c44c3145300f9f
ms.contentlocale: ja-jp
ms.lasthandoff: 06/03/2017

---
# <a name="change-your-mdm-authority"></a>MDM 機関を変更する
Configuration Manager バージョン 1610 および Microsoft Intune バージョン 1705 以降では、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除してから再登録しなくても、MDM 機関を変更することができます。

## <a name="change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する
ここでは、既存の管理対象デバイスの登録解除と再登録を行わずに、Configuration Manager コンソールから構成した既存の Microsoft Intune テナント (ハイブリッド) を Intune スタンドアロンに変更する方法について説明します。

### <a name="key-considerations"></a>主な考慮事項
新しい MDM 機関に変更した後、多くの場合、デバイスがチェックインしてサービスと同期されるまでに移行時間 (最大 8 時間) があります。 新しい MDM 機関 (Intune スタンドアロン) で、登録済みデバイスが変更後も管理および保護されるように設定を構成する必要があります。 」を参照し、次のことに注意してください。
- デバイスの既存の設定が新しい MDM 機関 (Intune スタンドアロン) の設定に置き換わるように、変更後にデバイスをサービスに接続する必要があります。
- MDM 機関を変更した後、最大 7 日間は、以前の MDM 機関 (ハイブリッド) の基本的な設定 (プロファイルなど) の一部がデバイスに残ります。 可能な限り早く新しい MDM 機関でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成し、既存の登録済みデバイスを使用するユーザーを含むユーザー グループにその設定を展開することをお勧めします。 MDM 機関の変更後、デバイスがサービスに接続すると、新しい MDM 機関の新しい設定がすぐに送信されるので、管理と保護の中断を回避できます。 新しいターゲットのポリシーがある場合は、デバイス上の既存のポリシーが上書きされます。
- 新しい MDM 機関に変更した後は、Microsoft Intune 管理コンソールのコンプライアンス データが正確に報告されるまでに最大 1 週間かかる可能性があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確なので、デバイスは引き続き保護されます。

### <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する準備
MDM 機関の変更に備えて、次の情報を確認します。
- MDM 機関を変更するオプションを使用するには、Configuration Manager バージョン 1610 以降が必要です。
- 新しい MDM 機関に変更した後に、デバイスがサービスに接続できるようになるまでに最大 8 時間かかります。
- MDM 機関の変更前に、ハイブリッドで現在管理されているすべてのユーザーに、Intune/EMS ライセンスが割り当てられていることを確認しておきます。 こうすることで、MDM 機関の変更後も、ユーザーとそのデバイスが Intune スタンドアロンで管理されます。 詳細については、「[ユーザー アカウントに Intune のライセンスを割り当てる](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4)」を参照してください。
- 管理者ユーザー アカウントに Intune/EMS ライセンスが割り当てられていること、管理者ユーザー アカウントが Intune にサインインできることを確認してから、MDM 機関を変更します。 Microsoft Intune 管理コンソールで、MDM 機関に **[Configuration Manager に設定]** (ハイブリッド テナント) と表示されることを確認してから、MDM 機関を変更します。
- Configuration Manager コンソールで、すべてのデバイス登録マネージャー ロールを削除します。 **[管理]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動し、Microsoft Intune サブスクリプションを選択し、**[プロパティ]**、**[デバイス登録マネージャー]** タブの順にクリックし、すべてのデバイス登録マネージャー ロールを削除します。
- Configuration Manager コンソールで既存のデバイス カテゴリを削除します。 **[資産とコンプライアンス]** > **[概要]** > **[デバイス コレクション]** の順に移動し、**[デバイス カテゴリの管理]** を選択し、既存のデバイス カテゴリを削除します。
- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 ただし、変更後すぐに、ユーザーがデバイスの電源を入れてサービスに接続するように、この変更について通知することをお勧めします。 こうすることで、多数のデバイスが迅速に新しい機関経由でサービスに接続し、登録できるようになります。
- Configuration Manager (ハイブリッド テナント) を使用して iOS デバイスを管理していて、MDM 機関を変更する予定の場合は、Configuration Manager で使用されていたものと同じ Apple Push Notification サービス (APNs) 証明書を更新し、Intune スタンドアロンでテナントのセットアップに使用する必要があります。

    > [!IMPORTANT]  
    > Intune スタンドアロンに別の APNs を使用する場合、以前に登録されていた iOS デバイスはすべて未登録になるので、デバイスを再登録するプロセスを実行する必要があります。 MDM 機関を変更する前に、Configuration Manager で iOS デバイスの管理に使用されていた APNs 証明書を正確に把握しておく必要があります。 Apple Push 証明書ポータル (https://identity.apple.com) に記載されているものと同じ証明書を検索し、元の APNs 証明書の作成に使用された Apple ID を持つユーザーを特定し、新しい MDM 機関を変更する際に同じ APNs 証明書を更新できることを確認します。  

### <a name="change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更する
MDM 機関を Intune スタンドアロンに変更するプロセスには、概要として次のような手順が含まれます。  
- Configuration Manager コンソールで **[MDM 機関を Microsoft Intune に変更]** オプションを使用して既存の Microsoft Intune サブスクリプションを削除します。
- Microsoft Intune 管理コンソールで新しい MDM 機関を **[Intune]** に設定します。
- 更新したものと同じ APNs 証明書を使用して、Apple APNs 証明書を構成します。
- 新しい MDM 機関 (Intune) から、Microsoft Intune 管理コンソールで新しい設定とアプリを構成し、展開します。
- 次にデバイスをサービスに接続すると、新しい MDM 機関と同期し、新しい設定を受信します。

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>MDM 機関を Intune スタンドアロンに変更するには
1.  Configuration Manager コンソールで **[管理]** &gt; **[概要]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune のサブスクリプション]** に移動し、既存の Intune サブスクリプションを削除します。
2.  **[MDM 機関を Microsoft Intune に変更]** を選択し、**[次へ]** をクリックします。

    ![APNs 証明書要求のダウンロード](/sccm/mdm/deploy-use/media/mdm-change-delete-subscription.png)
3.  Configuration Manager で MDM 機関を設定したときに元々使用していた Intune テナントにサインインします。
4.  **[次へ]** をクリックして、ウィザードを完了します。
5.  これで MDM 機関はリセットされました。 Configuration Manager コンソールの [Microsoft Intune サブスクリプション] ノードに Intune サブスクリプションは表示されなくなります。
6.  前の手順で使用したものと同じ Intune テナントを使用して、[Microsoft Intune 管理コンソール](http://manage.microsoft.com)にログインします。
7.  MDM 機関がリセットされたことを確認してから、MDM 機関を **[Microsoft Intune]** に設定します。 MDM 機関を変更すると、コンソールで反映されたことを確認できます。 詳細については、「[MDM 機関を設定する](https://docs.microsoft.com/en-us/intune/deploy-use/prerequisites-for-enrollment#step-2-set-mdm-authority)」を参照してください。
<!-- [Azure portal](https://docs.microsoft.com/en-us/intune-azure/enroll-devices/set-mdm-authority) -->


### <a name="configure-the-apns-certificate"></a>APNs 証明書を構成する
iOS デバイスがある場合は、Intune で APNs 証明書を構成する必要があります。

#### <a name="to-configure-the-apns-certificate"></a>APNs 証明書を構成するには
1.  APNs 証明書要求をダウンロードします。
    <!--The process is different depending on how you connect to Intune:
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment** &gt; **Apple MDM Push Certificate**, and then select **Download your CSR** to download and save the .csr file locally.   
    <br/>
    **Microsoft Intune administration console**   -->
    [Microsoft Intune 管理コンソール](http://manage.microsoft.com)で、**[管理]** &gt; **[モバイル デバイス管理]** &gt; **[iOS と Mac OS X]** &gt; **[APNs 証明書のアップロード]** に移動し、**[APNs 証明書要求のダウンロード]** を選択します。 証明書署名要求 (.csr) ファイルをローカルに保存します。
    > [!IMPORTANT]    
    > 新しい証明書署名要求をダウンロードする必要があります。 既存のファイルは使用しないでください。失敗します。

    ![APNs 証明書要求のダウンロード](/sccm/mdm/deploy-use/media/mdm-change-download-apns-certificate.png)

2.  [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) にアクセスし、以前に作成したときに使用したものと**同じ** Apple ID でサインインし、Configuration Manager (ハイブリッド) で使用していた APNs 証明書を更新します。

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Configuration Manager (ハイブリッド) で使用していた APNs 証明書を選択し、**[Renew]** をクリックします。   

    ![[Renew APNs] ダイアログ ボックス](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  ローカルにダウンロードした APNs 証明書署名要求 (.csr) ファイルを選択し、**[Upload]** をクリックします。

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  同じ APNs を選択し、**[Download]** をクリックします。 APNs (.pem) 証明書をダウンロードして、ファイルをローカルに保存します。  

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  以前と同じ Apple ID を使用して、更新された APNs 証明書を Intune テナントにアップロードします。
<!--The process is different depending on how to connect to Intune:  
    **Azure portal**   
    In the [Azure portal](https://azure.portal.com), choose **More Services** &gt; **Monitoring + Management** &gt; **Intune**. On the **Intune** blade, choose **Device enrollment** &gt; **Apple Enrollment**  &gt; **Apple MDM Push Certificate**, enter your Apple ID in step 3, select the certificate (.pem) file in step 4, and then click **Upload**.     
    <br/>
    **Microsoft Intune administration console**    -->
    In the [Microsoft Intune administration console](http://manage.microsoft.com), go to **Administration** &gt; **Mobile Device Management** &gt; **iOS and Mac OS X** &gt; **Upload an APNs Certificate**, and then choose **Upload the APNs certificate**. Go to the certificate (.pem) file, choose **Open**, and then enter your **Apple ID**.   

    ![Upload the APNs certificate](/sccm/mdm/deploy-use/media/mdm-change-upload-apns-certificate.png)

### <a name="next-steps"></a>次のステップ
MDM 機関の変更が完了したら、次の手順を実行します。
- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージを送信します (これは定期的にスケジュールされているチェックインとは別の操作です)。 そのため、テナントの MDM 機関がハイブリッドから Intune スタンドアロンに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、以降は Intune スタンドアロンに管理されるようになります。 これらのデバイスの管理と保護は中断されません。
- MDM 機関の変更中 (または変更直後) に電源を切っていたかオフラインだったデバイスは、電源を入れ、オンラインになったときに新しい MDM 機関のサービスに接続し、同期します。  

  iOS デバイスの場合、APNs 証明書の更新とセットアップのためにさらに時間が必要です。 そのため、iOS デバイスは最初のチェックイン要求を受信しません。 MDM 機関の変更中 (または変更直後) に iOS デバイスの電源が入り、オンラインだった場合でも、iOS デバイスが新しい MDM 機関のサービスに登録されるまでに最大 8 時間の遅れがあります (次の定期的なチェックインのタイミングに応じて異なります)。    

  > [!IMPORTANT]
  > MDM 機関を変更してから、更新された APNs 証明書が新しい機関にアップロードされるまで、iOS デバイスの新しいデバイスの登録とデバイスのチェックインは失敗します。 そのため、MDM 機関を変更した後は、できるだけ早く APNs 証明書を確認し、新しい機関にアップロードすることが重要です。   

- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、簡単にチェックインを開始できます。
- MDM 機関の変更後に、デバイスがサービスにチェックインして同期した後に、正常に動作していることを確認するには、[Microsoft Intune 管理コンソール](http://manage.microsoft.com)でそのデバイスを探します。 Configuration Manager (ハイブリッド) で管理されていたデバイスが、管理対象デバイスとして表示されるようになります。    
- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスを保護し、利用できるように、最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、次のものがデバイスに残ります。
    - 電子メール プロファイル
    - VPN プロファイル
    - 証明書プロファイル
    - Wi-Fi プロファイル
    - 構成プロファイル
- 既存の設定を上書きするための新しい設定は、古い設定が確実に上書きされるように、古い設定と同じ名前にする必要があります。 そうしないと、デバイスのプロファイルとポリシーが重複する可能性があります。
    > [!TIP]   
    > ベスト プラクティスとして、MDM 機関の変更が完了した直後に、すべての管理設定、構成、展開を作成することをお勧めします。 こうすることで、中間期間にもデバイスを保護し、アクティブに管理することができます。   
-  MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。   
    - 新しいデバイスを登録する
    - 新しく登録したデバイスが、Intune 管理コンソールに表示されることを確認します。
    - 管理コンソールからデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。

<!-- After the change in MDM authority and devices check-in with the service, note the following:      - The updated compliance status of devices will only display in the Azure portal immediately.
- There will be a delay for compliance status of devices to display in the Intune administrative console.-->


## <a name="change-the-mdm-authority-to-configuration-manager-hybrid"></a>MDM 機関を Configuration Manager (ハイブリッド) に変更する
ここでは、既存の管理対象デバイスの登録解除と再登録を行わずに、Intune から構成し、MDM 機関を Microsoft Intune (スタンドアロン) に設定した既存の **Microsoft Intune** テナントを、**Configuration Manager** (ハイブリッド) に変更する方法について説明します。

### <a name="key-considerations"></a>主な考慮事項
新しい MDM 機関に切り替えた後、多くの場合、デバイスがチェックインしてサービスと同期されるまでに移行時間 (最大 8 時間) があります。 新しい MDM 機関 (ハイブリッド) で、登録済みデバイスが変更後も管理および保護されるように設定を構成する必要があります。 」を参照し、次のことに注意してください。
- デバイスの既存の設定が新しい MDM 機関 (Intune スタンドアロン) の設定に置き換わるように、変更後にデバイスをサービスに接続する必要があります。
- MDM 機関を変更した後に、MDM 機関 (Intune スタンドアロン) の基本的な設定 (プロファイルなど) の一部は、最大 7 日間、またはデバイスが初めてサービスに接続するまで、デバイスに残ります。 可能な限り早く新しい MDM 機関 (ハイブリッド) でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成し、既存の登録済みデバイスがあるユーザーを含むユーザー グループにその設定を展開することをお勧めします。 MDM 機関の変更後、デバイスがサービスに接続すると、新しい MDM 機関の新しい設定がすぐに送信されるので、管理と保護の中断を回避できます。

### <a name="prepare-to-change-the-mdm-authority-to-configuration-manager-hybrid"></a>MDM 機関を Configuration Manager (ハイブリッド) に変更する準備
MDM 機関の変更に備えて、次の情報を確認します。
- MDM 機関を変更するオプションを使用するには、Configuration Manager バージョン 1610 以降が必要です。
- 新しい MDM 機関に変更した後に、デバイスがサービスに接続できるようになるまでに最大 8 時間かかります。
- Intune スタンドアロンで現在管理されているすべてのユーザーを含む Configuration Manager ユーザー コレクションを作成します。このユーザー コレクションは、Configuration Manager コンソールで Intune サブスクリプションをセットアップするときに使用します。 こうすることで、MDM 機関の変更互換モード、ユーザーとそのデバイスには Configuration Manager ライセンスが割り当てられ、ハイブリッド環境で管理されるようになります。
- このユーザー コレクションには、IT 管理者ユーザーも必ず含めます。  
- 変更前は、MDM 機関は Intune 管理コンソールで **[Microsoft Intune に設定]** \(スタンドアロン\) と表示されます。
- Microsoft Intune 管理コンソールで、MDM 機関に **[Microsoft Intune に設定]** \(スタンドアロン テナント\) と表示されることを確認してから、MDM 機関を変更します。
    > [!NOTE]    
    > MDM 機関に **[Managed by Intune and Office 365]\(Intune と Office 365 が管理\)** と表示される場合、MDM 機関を **Configuration Manager** (ハイブリッド) に変更すると、Office 365 で管理されていた MDM デバイスは管理されなくなります。 このようなユーザーには、MDM 機関を変更する前に、Intune または Enterprise Mobility Suite のライセンスを付与することをお勧めします。   

- [Microsoft Intune 管理コンソール](http://manage.microsoft.com)で、デバイス登録マネージャー ロールを削除します。 詳細については、「[Intune からのデバイス登録マネージャーの削除](/intune-classic/deploy-use/enroll-corporate-owned-devices-with-the-device-enrollment-manager-in-microsoft-intune#delete-a-device-enrollment-manager-from-intune)」を参照してください。
- 構成するデバイス グループ マッピングをオフにします。 詳細については、「[Microsoft Intune でデバイス グループのマッピングを使用してデバイスを分類する](/intune-classic/deploy-use/categorize-devices-with-device-group-mapping-in-microsoft-intune)」を参照してください。
- MDM 機関の変更中に、エンドユーザーへの影響はあまりありません。 ただし、変更後すぐに、ユーザーがデバイスの電源を入れてサービスに接続するように、この変更について通知することをお勧めします。 こうすることで、多数のデバイスが迅速に新しい機関経由でサービスに接続し、登録できるようになります。
- Intune スタンドアロンを使用して iOS デバイスを管理していて、MDM 機関を変更する予定の場合は、Intune で使用されていたものと同じ Apple Push Notification サービス (APNs) 証明書を更新し、Configuration Manager (ハイブリッド) でテナントのセットアップに使用する必要があります。    

    > [!IMPORTANT]  
    > ハイブリッドに別の APNs を使用する場合、以前に登録されていた iOS デバイスはすべて未登録になるので、デバイスを再登録するプロセスを実行する必要があります。 MDM 機関を変更する前に、Intune で iOS デバイスの管理に使用されていた APNs 証明書を正確に把握しておく必要があります。 Apple Push 証明書ポータル (https://identity.apple.com) に記載されているものと同じ証明書を検索し、元の APNs 証明書の作成に使用された Apple ID を持つユーザーを特定し、新しい MDM 機関を変更する際に同じ APNs 証明書を更新できることを確認します。  

### <a name="change-the-mdm-authority-to-configuration-manager"></a>MDM 機関を Configuration Manager に変更する
MDM 機関を Configuration Manager (ハイブリッド) に変更するプロセスには、概要として次のような手順が含まれます。  
- Configuration Manager コンソールで、Microsoft Intune サブスクリプションを追加します。
- 更新したものと同じ APNs 証明書を使用して、Apple APNs 証明書を構成します。
- Configuration Manager コンソールで、新しい MDM 機関 (ハイブリッド) から新しい設定とアプリを構成し、展開します。
- 次にデバイスをサービスに接続すると、新しい MDM 機関と同期し、新しい設定を受信します。

#### <a name="to-change-the-mdm-authority-to-configuration-manager"></a>MDM 機関を Configuration Manager に変更するには
1.  Configuration Manager コンソールで **[管理]** &gt; **[概要]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、Intune サブスクリプションを選択して追加します。
2.  Intune で MDM 機関を設定したときに元々使用していた Intune テナントにサインインし、**[次へ]** をクリックします。
3.  **[MDM 機関を Configuration Manager に変更]** を選択し、**[次へ]** をクリックします。
4.  新しいハイブリッド MDM 機関で継続して管理するすべてのユーザーを含むユーザー コレクションを選択します。
5.  **[次へ]** をクリックして、ウィザードを完了します。  
5.  これで MDM 機関は **Configuration Manager** に変更されました。
6.  同じ Intune テナントを使用して [Microsoft Intune 管理コンソール](http://manage.microsoft.com)にログインし、MDM 機関が **[Configuration Manager に設定]** に変更されたことを確認します。


### <a name="enable-ios-enrollment"></a>iOS の登録を有効にします。
iOS デバイスがある場合は、Configuration Manager で APNs 証明書を構成する必要があります。

#### <a name="to-enable-ios-enrollment-and-configure-the-apns-certificate"></a>iOS の登録を有効にして APNs 証明書を構成するには

1. **証明書署名要求のダウンロード**

    1.  Configuration Manager コンソールで、**[管理]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、**[APNs 証明書要求の作成]** を選択して **[Apple Push Notification Service 証明書署名要求の要求]** ダイアログ ボックスを開きます。  
    2.  **[参照]** をクリックして、新しい証明書署名要求 (.csr) ファイルの保存先のパスを指定します。 証明書署名要求 (.csr) ファイルをローカルに保存します。  
    3.  **[ダウンロード]**をクリックします。 新しい Microsoft Intune .csr ファイルがダウンロードされ、Configuration Manager によって保存されます。   

    > [!IMPORTANT]
    > 新しい証明書署名要求をダウンロードする必要があります。 既存のファイルは使用しないでください。失敗します。  

2.  [Apple Push Certificates Portal](http://go.microsoft.com/fwlink/?LinkId=269844) にアクセスし、以前に作成したときに使用したものと**同じ** Apple ID でサインインし、Intune スタンドアロンで使用していた APNs 証明書を更新します。

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-apns-portal.png)

3.  Intune スタンドアロンで使用していた APNs 証明書を選択し、**[Renew]** をクリックします。   

    ![[Renew APNs] ダイアログ ボックス](/sccm/mdm/deploy-use/media/mdm-change-renew-apns.png)

4.  ローカルにダウンロードした APNs 証明書署名要求 (.csr) ファイルを選択し、**[Upload]** をクリックします。

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-upload.png)  
5.  同じ APNs を選択し、**[Download]** をクリックします。 APNs (.pem) 証明書をダウンロードして、ファイルをローカルに保存します。  

    ![Apple Push Certificates Portal のサインイン ページ](/sccm/mdm/deploy-use/media/mdm-change-renew-apns-download.png)

6.  以前と同じ Apple ID を使用して、更新された APNs 証明書をハイブリッド テナントにアップロードします。

    1.  Configuration Manager コンソールで **[管理]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、**[プラットフォームの構成]** &gt; **[iOS]** の順に選択します。  
    2.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスで、**[APNs 証明書]** タブを選択し、**[iOS と Mac OS X (MDM) の登録を有効にする]** チェックボックスをオンにします。  
    3.  **[参照]**をクリックし、Apple からダウンロードした APNs 証明書 (.cer) ファイルに移動します。 Configuration Manager に APNs 証明書情報が表示されます。 **[OK]** をクリックして、APNs 証明書を Intune に保存します。  

        ![[Microsoft Intune サブスクリプションのプロパティ] ページ - iOS](/sccm/mdm/deploy-use/media/mdm-change-subscription-properties-ios.png)

### <a name="enable-android-enrollment"></a>Android の登録を有効にする
1. Configuration Manager コンソールで **[管理]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、**[プラットフォームの構成]** &gt; **[Android]** の順に選択します。  
2. **[Android の登録を有効にする]** を選択し、**[OK]** をクリックします。

### <a name="enable-windows-enrollment"></a>Windows の登録を有効にする
1. Configuration Manager コンソールで **[管理]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、**[プラットフォームの構成]** &gt; **[Windows]** の順に選択します。  
2. **[Windows の登録を有効にする]** を選択し、**[OK]** をクリックします。

### <a name="enable-windows-phone-enrollment"></a>Windows Phone の登録を有効にする
1. Configuration Manager コンソールで **[管理]** &gt; **[クラウド サービス]** &gt; **[Microsoft Intune サブスクリプション]** に移動し、**[プラットフォームの構成]** &gt; **[Windows Phone]** の順に選択します。  
2. 有効にするプラットフォームを選択し、**[OK]** をクリックします。


### <a name="next-steps"></a>次のステップ
MDM 機関の変更が完了したら、次の手順を実行します。
- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期するように促す通知メッセージを送信します (これは定期的にスケジュールされているチェックインとは別の操作です)。 そのため、テナントの MDM 機関が Intune スタンドアロンからハイブリッドに変更された後は、電源を入れてオンラインになったすべてのデバイスはサービスに接続し、新しい MDM 機関を受信し、以降はハイブリッドに管理されるようになります。 これらのデバイスの管理と保護は中断されません。
- MDM 機関の変更中 (または変更直後) にデバイスの電源が入り、オンラインだった場合でも、デバイスが新しい MDM 機関のサービスに登録されるまでに最大 8 時間の遅れがあります (次の定期的なチェックインのタイミングに応じて異なります)。    

  > [!IMPORTANT]
  > MDM 機関を変更してから、更新された APNs 証明書が新しい機関にアップロードされるまで、iOS デバイスの新しいデバイスの登録とデバイスのチェックインは失敗します。 そのため、MDM 機関を変更した後は、できるだけ早く APNs 証明書を確認し、新しい機関にアップロードすることが重要です。

- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、簡単にチェックインを開始できます。
- MDM 機関の変更後に、デバイスがサービスにチェックインして同期した後に、正常に動作していることを確認するには、Configuration Manager コンソールでそのデバイスを探します。 Intune で管理されていたデバイスが、Configuration Manager で管理対象デバイスとして表示されるようになります。    
- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスを保護し、利用できるように、最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、次のものがデバイスに残ります。
    - 電子メール プロファイル
    - VPN プロファイル
    - 証明書プロファイル
    - Wi-Fi プロファイル
    - 構成プロファイル
- 新しい MDM 機関に変更した後は、Microsoft Intune 管理コンソールのコンプライアンス データが正確に報告されるまでに最大 1 週間かかる可能性があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確なので、デバイスは引き続き保護されます。
- 既存の設定を上書きするための新しい設定は、古い設定が確実に上書きされるように、古い設定と同じ名前にする必要があります。 そうしないと、デバイスのプロファイルとポリシーが重複する可能性があります。
    > [!TIP]   
    > ベスト プラクティスとして、MDM 機関の変更が完了した直後に、すべての管理設定、構成、展開を作成することをお勧めします。 こうすることで、中間期間にもデバイスを保護し、アクティブに管理することができます。   
-  MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。   
    - 新しいデバイスを登録する
    - 新しく登録したデバイスが、Configuration Manager コンソールに表示されることを確認します。
    - 管理コンソールからデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。

