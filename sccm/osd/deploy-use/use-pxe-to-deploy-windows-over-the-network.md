---
title: "PXE を使用したネットワーク経由での Windows の展開 | Microsoft ドキュメント"
description: "PXE によるオペレーティング システムの展開を使用して、コンピューターのオペレーティング システムを更新するか、新しいコンピューターに新しいバージョンの Windows をインストールします。"
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: b88ab3799027c78a8c605e934b247097b31e1d21
ms.contentlocale: ja-jp
ms.lasthandoff: 06/28/2017


---
# System Center Configuration Manager で PXE を使用してネットワーク経由で Windows を展開する
<a id="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager での PXE (Preboot execution environment) によるオペレーティング システムの展開では、クライアント コンピューターはネットワーク経由でオペレーティング システムを要求し、展開することができます。 この展開シナリオでは、オペレーティング システム イメージ、および x86 と x64 の Windows PE ブート イメージを、PXE ブート要求を許可するように構成された配布ポイントに送信します。

> [!NOTE]  
>  x64 BIOS コンピューターのみを対象とするオペレーティング システムの展開を作成する場合は、配布ポイントに x64 ブート イメージと x86 ブート イメージの両方を用意する必要があります。

次のオペレーティング システムの展開シナリオでは、PXE によるオペレーティング システムの展開を使用できます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

いずれかのオペレーティング システムの展開シナリオのステップを完了させてから、次のセクションを参照して、PXE による展開を準備します。

##  <a name="BKMK_Configure"></a> PXE 要求を許可するために少なくとも 1 つの配布ポイントを構成する
PXE ブート要求を作成するクライアントにオペレーティング システムを展開するには、PXE ブート要求に応答するように構成された 1 つ以上の配布ポイントを使用します。 配布ポイントで PXE を有効にする手順については、「[PXE 要求を受け入れるための配布ポイントの構成](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)」を参照してください。

## PXE 対応のブート イメージの作成
<a id="prepare-a-pxe-enabled-boot-image" class="xliff"></a>
PXE を使用してオペレーティング システムを展開するには、1 つ以上の PXE 対応配布ポイントに配布される、x86 と x64 の両方の PXE 対応ブート イメージが必要です。 この情報を使用して、ブート イメージで PXE を有効にして、配布ポイントにブート イメージを配布します。

-   ブート イメージで PXE を有効にするには、**[データ ソース]** タブのブート イメージ プロパティで、**[このブート イメージを PXE 対応の配布ポイントから展開する]** を選択します。

-   ブート イメージのプロパティを変更する場合は、再配布ポイントにブート イメージを再配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)」をご覧ください。

##  <a name="BKMK_PXEExclusionList"></a> PXE 展開の除外リストの作成
PXE を使用してオペレーティング システムを展開する場合、配布ポイントで除外リストを作成できます。 除外リストには、配布ポイントが無視すべきコンピューターの MAC アドレスを追加します。 リストに追加されたコンピューターは、Configuration Manager が PXE 展開で使用する展開タスク シーケンスを受け取りません。

#### 除外リストを作成するには
<a id="to-create-the-exclusion-list" class="xliff"></a>

1.  PXE 対応の配布ポイントにテキスト ファイルを作成します。 例として、このテキスト ファイルを **pxeExceptions.txt**と名づけます。

2.  メモ帳などのプレーン テキスト エディターを使用して、PXE 対応配布ポイントが無視するべきコンピューターの MAC アドレスを追加します。 MAC アドレス値はコロンを使って区切り、各アドレスを別の行に入力します。 例: `01:23:45:67:89:ab`

3.  PXE 対応の配布ポイント サイト システム サーバーにテキスト ファイルを保存します。 テキスト ファイルはサーバーの任意の場所に保存できます。

4.  PXE 対応配布ポイントのレジストリを編集して、**MACIgnoreListFile** レジストリ キーを作成します。 PXE 対応の配布ポイント サイト システム サーバーでテキスト ファイルのフル パスの文字列値を追加します。 次のレジストリ パスを使用します。

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  レジストリ エディターの使用方法を誤ると、重大な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 レジストリ エディターの使用方法を誤った結果生じた問題については、解決できる保証はありません。 レジストリ エディターは、ご自身の責任において使用してください。

     このレジストリの変更を行った後、サーバーの再起動は必要ありません。

##  <a name="BKMK_RamDiskTFTP"></a>RamDisk TFTP ブロック サイズとウィンドウ サイズ
Configuration Manager バージョン 1606 では、PXE 対応配布ポイントの RamDisk TFTP ブロック サイズとウィンドウ サイズをカスタマイズできます。 ネットワークをカスタマイズしている場合、ブロックまたはウィンドウのサイズが大きすぎるために、ブート イメージのダウンロードがタイムアウト エラーで失敗する可能性があります。 RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズにより、特定のネットワーク要件に対応する PXE を使用する場合に、TFTP トラフィックを最適化できます。 最も効率的な方法を確認するために、環境内でカスタマイズした設定をテストします。 詳細については、「[PXE 対応配布ポイント上の RamDisk TFTP ブロック サイズとウィンドウ サイズのカスタマイズ](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP)」を参照してください。

## 展開の設定の構成
<a id="configure-deployment-settings" class="xliff"></a>
PXE によるオペレーティング システムの展開を使用する場合、オペレーティング システムを PXE ブート要求から使用できるように展開を構成する必要があります。 ソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで使用可能なオペレーティング システムを構成することができます。 **[利用できるようにする項目]** の設定では、次のいずれかを設定します。

-   Configuration Manager クライアント、メディア、PXE

-   メディアと PXE のみ

-   メディアと PXE のみ (非表示)

##  <a name="BKMK_Deploy"></a> タスク シーケンスの展開
オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。 PXE を使用してオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。

-   **必要な展開**: 必要な展開では、ユーザーの介入なしに、PXE を使用します。 ユーザーは PXE ブートをバイパスできません。 しかし、ユーザーが配布ポイントが応答する前に PXE ブートをキャンセルすれば、オペレーティング システムは展開されません。

-   **利用可能な展開**: 利用可能な展開では、PXE ブート プロセスを続けるために F12 キーを押すユーザーがセットアップ先のコンピューターにいる必要があります。 F12 を押すユーザーがいない場合、コンピューターは現在のオペレーティング システム、または次に利用可能なブート デバイスから起動します。

Configuration Manager コレクションまたはコンピューターに割り当てられた最終の PXE 展開の状態をクリアすることにより、必要な PXE 展開を再展開することができます。 この操作でその展開の状態がリセットされ、最新の必要な展開が再インストールされます。

> [!IMPORTANT]
> PXE プロトコルはセキュリティ保護されていません。 PXE サーバーと PXE クライアントのどちらも、サイトへの不正なアクセスを防御するデータセンターといった物理的に安全なネットワークに置かれていることを確認します。

##  PXE ブートのクライアントが使用するブート イメージの選択方法
<a id="how-is-the-boot-image-selected-for-clients-booting-with-pxe" class="xliff"></a>
クライアントが PXE で起動する場合、使用するブート イメージが Configuration Manager によってクライアントに提供されます。 Configuration Manager バージョン 1606 以降、Configuration Manager は、アーキテクチャが厳密に一致するブート イメージを使用します。 正確なアーキテクチャのブート イメージがない場合、Configuration Manager は、互換性のあるアーキテクチャを持つブート イメージを使用します。 次の一覧では、PXE ブートのクライアントが使用するブート イメージがどのように選択されるかについて説明します。
1. Configuration Manager は、ブートしようとしているクライアントの MAC アドレスまたは SMBIOS に一致するシステム レコードをサイト データベースで検索します。  

    > [!NOTE]
    > サイトに割り当てられているコンピューターを、別のサイトの PXE にブートした場合、そのコンピューターでポリシーを表示できません。 たとえば、クライアントが既にサイト A に割り当てられている場合、サイト B の管理ポイントと配布ポイントは、サイト A のポリシーにアクセスできず、クライアントは正常に PXE ブートしません。

2. Configuration Manager は、手順 1 で見つかったシステム レコードに展開されているタスク シーケンスを探します。

3. 手順 2 で見つかったタスク シーケンスの一覧で、Configuration Manager はブートしようとしているクライアントのアーキテクチャに一致するブート イメージを探します。 同じアーキテクチャのブート イメージが見つかった場合は、そのブート イメージを使用します。

4. 同じアーキテクチャのブート イメージが見つからなかった場合、Configuration Manager は、クライアントのアーキテクチャと互換性があるブート イメージを探します。 手順 2. で見つかったタスク シーケンスの一覧で探します。 たとえば、64 ビット クライアントは、32 ビットおよび 64 ビットのブート イメージと互換性があります。 32 ビット クライアントは、32 ビットのブート イメージのみと互換性があります。 UEFI クライアントは、64 ビットのブート イメージのみと互換性があります。

