---
title: "Updates Publisher のインストール | Microsoft Docs"
description: "環境に System Center Updates Publisher をインストールする"
ms.custom: na
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 70772ba7d08560aa66abcce29dc6cc6334aa2032
ms.openlocfilehash: 63ea0383497a3f06870c0907c732010259d1a809
ms.contentlocale: ja-jp
ms.lasthandoff: 07/03/2017

---
# <a name="install-updates-publisher"></a>Updates Publisher のインストール

*適用対象: System Center Updates Publisher*

このトピックの情報を参考にすると、お使いの環境で使用する Updates Publisher を取得、インストール、セットアップできます。


## <a name="prerequisites-and-limitations"></a>前提条件と制限事項
次のセクションでは、Updates Publisher をインストールして使用するための要件と、使用に際しての制限事項や既知の問題について詳しく説明します。

### <a name="operating-systems"></a>オペレーティング システム
次のオペレーティング システムの 64 ビット版に、Updates Publisher をインストールして実行します。 累積的な更新プログラムや Service Pack は不要です。

-   Windows Server 2016 (Standard、Datacenter)
-   Windows Server 2012 R2 (Standard、Datacenter)
-   Windows 10 (Pro、Education、Pro Education、Enterprise)
-   Windows 8.1 (Professional、Enterprise)

### <a name="prerequisites"></a>必要条件
Updates Publisher を実行するコンピューターには、以下のものが必要です。

-   **64 ビット オペレーティング システム**: Updates Publisher をインストールするコンピューターは、64 ビット版のオペレーティング システムで動作している必要があります。
-   **WSUS 4.0 以降**:
    -   この要件を満たすために、Windows Server に既定の管理コンソールをインストールします。
    -   Windows 10 と Windows 8.1 の場合は、[Windows オペレーティング システム用のリモート サーバー管理ツール (RSAT)](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems) をインストールします。 これにより、Updates Publisher を使用するために必要なサポート (*API と PowerShell コマンドレット*、*ユーザー インターフェイス管理コンソール*) がインストールされます。
-   **アクセス許可**:
    -   インストール: ローカル管理者
    -   ほとんどの操作: ローカル ユーザー
    -   発行または WSUS に関連する操作: WSUS サーバー上の WSUS 管理者グループのメンバー

### <a name="supported-languages"></a>サポートされる言語
Updates Publisher で使用できる言語は英語のみですが、他言語向けの更新プログラムを管理できます。 言語サポートは、更新プログラムの発行、作成、編集などのタスクによって異なります。

更新プログラムをエクスポートまたは発行するとき、Updates Publisher は Updates Publisher がインストールされているコンピューターのロケール設定に基づいて、ソフトウェア更新プログラムのタイトルと説明を表示します。

たとえば、英語とスペイン語のタイトルを持つソフトウェア更新プログラムを作成します。

-   ロケール設定が英語 (既定) になっているコンピューターで更新プログラムを作成すると、英語でタイトルと説明が表示されます。
-   次に、ロケール設定がスペイン語になっているコンピューターに対して更新プログラムをエクスポートまたは発行すると、そのコンピューター上ではタイトルと説明がスペイン語で表示されます。

### <a name="publishing"></a>発行
ソフトウェア更新プログラムを発行するときに、ソフトウェア更新プログラムのバイナリ ファイルの言語を指定できます。 バイナリが言語に依存しないように指定することもできます。 次の言語がサポートされています。

-   アラビア語
-   中国語 (香港: 中華人民共和国香港特別行政区)
-   繁体字中国語
-   中国語 (簡体字)
-   チェコ語
-   デンマーク語
-   オランダ語
-   英語
-   フィンランド語
-   フランス語
-   ドイツ語
-   ギリシャ語
-   ヘブライ語
-   ハンガリー語
-   イタリア語
-   日本語
-   韓国語
-   ノルウェー語
-   ポーランド語
-   ポルトガル語
-   ポルトガル語 (ブラジル)
-   ロシア語
-   スペイン語
-   スウェーデン語
-   トルコ語

### <a name="software-update-titles-and-descriptions"></a>ソフトウェア更新プログラムのタイトルと説明
ソフトウェア更新プログラムのタイトルと説明については、次の言語がサポートされています。

-   繁体字中国語
-   中国語 (簡体字)
-   英語
-   フランス語
-   ドイツ語
-   イタリア語
-   日本語
-   韓国語
-   ポルトガル語 (ブラジル)
-   ロシア語
-   スペイン語



## <a name="install-updates-publisher"></a>Updates Publisher のインストール
[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?linkid=847967)から、System Center Updates Publisher をインストールするための **UpdatesPubliser.msi** を取得します。

Updates Publisher をインストールするには、上記の*前提条件*を満たしているコンピューター上で **UpdatesPublisher.msi** を実行します。 インストーラーは、Updates Publisher を実行するために必要なファイルを格納する次のフォルダーを作成します: *&lt;path&gt;\Program Files\Microsoft\UpdatesPublisher*。

このフォルダーには Updates Publisher を使用するために必要なすべてのファイルが格納されるため、そのフォルダーとファイルを新しい場所またはコンピューターにコピーすれば、その場所から Updates Publisher を使用できます。 ただし、新しい場所またはコンピューターは、Updates Publisher を実行するための前提条件を満たしている必要があります。

インストールが完了したら、*UpdatesPublisher* フォルダーにある **UpdatesPublisher.exe** を実行して、Updates Publisher を開始します。

## <a name="next-steps"></a>次のステップ
 Updates Publisher のインストールが完了したら、Updates Publisher の[オプションを構成する](updates-publisher-options.md)ことをお勧めします。 Updates Publisher の一部の機能を使用するためには、オプションを構成する必要があります。

 ただし、更新サーバーや管理対象デバイスに更新プログラムを展開するつもりがなく、既定のままで使用する場合は、[ソフトウェア更新カタログの管理](updates-publisher-catalogs.md)または[ソフトウェア更新プログラムの作成](create-updates-with-updates-publisher.md)に進んで、ご自身の更新カタログを作成できます。

