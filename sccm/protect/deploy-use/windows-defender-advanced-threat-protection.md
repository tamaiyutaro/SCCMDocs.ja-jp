---
title: "Windows Defender Advanced Threat Protection | Microsoft ドキュメント"
description: "企業が高度な攻撃に対応するための新しいサービスである Windows Defender Advanced Threat Protection を管理および監視する方法について説明します。"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ebda27c0f3848615346c2ecf1ab8b9bb9ab6f0d
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.contentlocale: ja-jp
ms.lasthandoff: 05/26/2017

---
# Windows Defender Advanced Threat Protection
<a id="windows-defender-advanced-threat-protection" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager のバージョン 1606 (Current Branch) 以降、Endpoint Protection を使用して、Windows Defender Advanced Threat Protection (ATP) を管理および監視できるようになりました。 Windows Defender ATP は、企業が自社のネットワークに対する高度な攻撃を検出して調査し、対応するのに役立つ新しいサービスです。  Windows Defender ATP の詳細は、[こちら](http://aka.ms/technet-wdatp)をご覧ください。 Configuration Manager ポリシーは、管理対象となる Windows 10 バージョン 1607 (ビルド 14328) 以降の登録と監視に役立ちます。

Windows Defender ATP は、[Windows セキュリティ センター](https://securitycenter.windows.com)のサービスです。 Configuration Manager は、クライアントのオンボード構成ファイルを追加して展開することにより、展開の状態と Windows Defender ATP エージェントの正常性を監視できます。 Windows Defender ATP は、構成マネージャー クライアントを実行するコンピューターでのみサポートされます。 オンプレミス モバイル デバイス管理と Intune ハイブリッド MDM で管理されたコンピューターはサポートされていません。

 **必要条件**  

-   Windows Defender Advanced Threat Protection オンライン サービスのサブスクリプション  
-   Windows 10 バージョン 1607 以降を実行しているクライアント コンピューター  
-   Configuration Manager 1610 バージョン以降のクライアント エージェントを実行しているクライアント コンピューター

## オンボード構成ファイルの作成方法
<a id="how-to-create-an-onboarding-configuration-file" class="xliff"></a>  

 1.  [Windows Defender ATP オンライン サービス](https://securitycenter.windows.com/)にログオンします。   

 2.  **[Endpoint Management]**(エンドポイント管理) メニュー項目を開きます。  

 3.  **[System Center Configuration Manager (current branch) version 1606]** を選択し、**[Download package]**(パッケージのダウンロード) をクリックします。  

 4.  圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。

> [!IMPORTANT]
> Windows Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。

## Windows Defender ATP のオンボード デバイス
<a id="onboard-devices-for-windows-defender-atp" class="xliff"></a>  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[Endpoint Protection]** > **[Windows Defender ATP ポリシー]** の順に移動し、**[Windows Defender ATP ポリシーの作成]** をクリックします。 Windows Defender ATP ポリシーの作成ウィザードが開きます。  

2.  Windows Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、**[オンボード]** を選択します。 [ **次へ** ] をクリックします。  

3.  組織の Windows Defender ATP のクラウド サービス テナントによって提供される構成ファイルを**参照**します。 [ **次へ** ] をクリックします。  

4.  管理対象のデバイスから分析用に収集され共有されるファイルのサンプルを指定します。  

    -   **なし**   

    -   **すべてのファイルの種類**  

     [ **次へ** ] をクリックします。  

5.  概要を確認して、ウィザードを完了します。  

6.  これで、**[展開]** をクリックすると、Windows Defender ATP ポリシーを管理対象のクライアント コンピューターに展開できます。  

## Windows Defender ATP の監視
<a id="monitor-windows-defender-atp" class="xliff"></a>  

1.  Configuration Manager コンソールで、**[監視]** > **[概要]** > **[セキュリティ]** の順に移動し、**[Windows Defender ATP]** をクリックします。  

2.  Windows Defender Advanced Threat Protection ダッシュボードを確認します。  

    -   **Windows Defender のエージェントの展開ステータス**: アクティブな Windows Defender ATP ポリシーがオンボードされている管理対象のクライアント コンピューターの数と割合  

    -   **Windows Defender ATP エージェントの正常性**: 自身の Windows Defender ATP エージェントの状態を報告するコンピューター クライアントの割合  

        -   **正常**: 正常に機能しています  

        -   **非アクティブ**: 期間中にサービスに送信されるデータがありません  

        -   **エージェントの状態**: Windows でエージェントのシステム サービスが実行されていません  

        -   **非オンボード**: ポリシーは適用されましたが、エージェントがポリシー オンボードを報告していません  


## オフボード構成ファイルの作成および展開方法
<a id="how-to-create-and-deploy-an-offboarding-configuration-file" class="xliff"></a>  

1.  [Windows Defender ATP オンライン サービス](https://securitycenter.windows.com/)にログオンします。   

2.  **[Endpoint Management]**(エンドポイント管理) メニュー項目を開きます。  

3.  **[System Center Configuration Manager (current branch) version 1606]** を選択し、**[Endpoint offboarding]**(エンドポイント オフボード) をクリックします。  

4.  圧縮済みアーカイブ (.zip) ファイルをダウンロードして内容を抽出します。 オフボード ファイルは、30 日間有効です。

5.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[Endpoint Protection]** > **[Windows Defender ATP ポリシー]** の順に移動し、**[Windows Defender ATP ポリシーの作成]** をクリックします。 Windows Defender ATP ポリシーの作成ウィザードが開きます。  

6.  Windows Defender ATP ポリシーの **[名前]** と **[説明]** を入力し、**[オフボード]** を選択します。 **[次へ]**をクリックします。  

7.  組織の Windows Defender ATP のクラウド サービス テナントによって提供される構成ファイルを**参照**します。 **[次へ]**をクリックします。  

8.  概要を確認して、ウィザードを完了します。  

9.  これで、**[展開]** をクリックすると、Windows Defender ATP ポリシーを管理対象のクライアント コンピューターに展開できます。  

> [!IMPORTANT]
> Windows Defender ATP 構成ファイルには、セキュリティで保護する必要がある機密情報が含まれています。

[Windows Defender Advanced Threat Protection](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Windows Defender Advanced Threat Protection のオンボードの問題のトラブルシューティング](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)

