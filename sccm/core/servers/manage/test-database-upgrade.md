---
title: "データベース更新のテスト | Microsoft Docs"
description: "Configuration Manager 用の更新プログラムをインストールする際に、サイト データベースのアップグレードをテストします。"
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 6b76c97cd205bb02683a7bfa1eb378471a75551d
ms.contentlocale: ja-jp
ms.lasthandoff: 06/13/2017


---
# 更新プログラムをインストールする際にデータベース アップグレードをテストする
<a id="test-the-database-upgrade-when-installing-an-update" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックの情報は、現在のブランチの Configuration Manager 用のコンソール内の更新プログラムをインストールする前にデータベース アップグレードのテストを実行するのに役立ちます。 ただし、データベースが未確認である場合や、Configuration Manager で明示的にサポートされていないカスタマイズで変更されている場合を除き、アップグレードのテストは必須の手順あるいは推奨される手順ではなくなりました。

## アップグレードのテストを実行する必要がありますか?
<a id="do-i-need-to-run-a-test-upgrade" class="xliff"></a>
このアップグレードのテストは、System Center Configuration Manager で導入される変更に伴い、非推奨となります。 これらの変更により、プロセスが簡略化され、実稼働環境を新しいバージョンに短時間で更新できるようになります。 この再設計の目的は、常にお客様のリスクを軽減し、新しい更新プログラムをそれぞれインストールする際の運用のオーバーヘッドを減らせるようにすることです。

サイトの回復を実行することなく、失敗した更新プログラムを自動的にロールバックするロジックを含む、更新プログラムのインストール方法が変更されています。 これらの変更により、コンソールを使用して、更新プログラムのインストールを管理できるようになります。また、これらの変更には、[失敗した更新プログラムのインストールを再試行する](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry)オプションが含まれます。

> [!TIP]
> System Center 2012 Configuration Manager などの古い製品から System Center Configuration Manager にアップグレードする場合、[データベース アップグレードのテストは引き続き推奨される手順](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#a-namebkmktesta-test-the-site-database-upgrade)です。

コンソール内の更新プログラムをインストールするときでもサイト データベースのアップグレードをテストする予定の場合、以下の情報は[コンソール内更新プログラムのインストールに関するガイダンス](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)を補足するものとなります。

## データベース アップグレードのテストを実行するための準備
<a id="prepare-to-run-a-test-database-upgrade" class="xliff"></a>  
1702 の更新など、階層内に新しい更新プログラムをインストールする前に、サイト データベースのアップグレードをテストできます。

アップグレードのテストを実行するには、更新対象バージョンの Configuration Manager を実行しているサイトの [CD.Latest フォルダー](/sccm/core/servers/manage/the-cd.latest-folder)にあるソース ファイルの Configuration Manager セットアップを使用します。 この要件は、1702 に更新するためにデータベースの更新をテストすることを意味します。
-   CD.Latest フォルダーを取得できる、バージョン 1702 を実行する 1 つ以上のサイトが必要です。
-   必要なバージョンを実行するサイトがない場合は、ラボ環境でのサイトのインストールを検討し、そのサイトを新しいバージョンに更新します。 これにより、正しいバージョンのソース ファイルを含む CD.Latest フォルダーを作成することができます。

アップグレードのテストは、SQL Server の別のインスタンスに復元したサイト データベースのバックアップに対して実行されます。  データベースのコピーを復元したアップグレードをテストするには、**testdbupgrade** コマンド ライン スイッチを使用して **CD.Latest** フォルダーからセットアップを実行します。 アップグレード テストの完了後、アップグレードされたデータベースは破棄されます。 これを Configuration Manager サイトで使用することはできません。

更新プログラムのインストールが失敗した場合に、サイトを回復する必要はありません。 代わりに、コンソール内から更新プログラムのインストールを再試行できます。

##  アップグレードのテストを実行する
<a id="run-the-test-upgrade" class="xliff"></a>    
1.  Configuration Manager セットアップと、更新する予定のバージョンを実行するサイトの **CD.Latest** フォルダーにあるソース ファイルを使用します。  

2.  データベース アップグレードのテストを実行するために使用する SQL Server インスタンスの場所に **CD.Latest** フォルダーをコピーします。

3.  アップグレードをテストするサイト データベースのバックアップを作成します。 次に、Configuration Manager サイトをホストしていない SQL Server のインスタンスにそのデータベースのコピーを復元します。 SQL Server インスタンスは、サイト データベースと同じエディションの SQL Server を使用する必要があります。  

4.  データベースのコピーを復元したら、更新するバージョンのソース ファイルを含む CD.Latest フォルダーから**セットアップ**を実行します。 セットアップを実行する際は、 **/TESTDBUPGRADE** コマンド ライン オプションを使います。 データベースのコピーをホストする SQL Server インスタンスが既定のインスタンスでない場合は、コマンドライン引数を指定して、サイト データベースのコピーをホストするインスタンスを識別します。   

  たとえば、データベース名が *SMS_ABC* のサイト データベースがあるとします。 このサイト データベースのコピーを、インスタンス名が *DBTest* の SQL Server のサポートされているインスタンスに復元します。 このサイト データベースのコピーのアップグレードをテストするには、**Setup.exe /TESTDBUPGRADE DBtest\CM_ABC** というコマンド ラインを使用します。  

  Setup.exe は、System Center Configuration Manager のソース メディアの **SMSSETUP\BIN\X64** にあります。  

5.  アップグレード テストを実行する SQL Server インスタンスで、システム ドライブのルート内の *ConfigMgrSetup.log* を確認し、進行状況と成功状態を監視します。  

     アップグレード テストに失敗した場合は、サイト データベースのアップグレード失敗に関する問題をすべて修正します。 次に、サイト データベースの新しいバックアップを作成し、データベースの新しいコピーのアップグレードをテストします。  



## 次のステップ
<a id="next-steps" class="xliff"></a>
データベースの更新テストが正常に完了したら、更新されたデータベースを破棄します。 これを Configuration Manager サイトで使用することはできません。 その後、アクティブなサイトに戻り、[更新プログラムのインストール](/sccm/core/servers/manage/install-in-console-updates)を開始できます。

