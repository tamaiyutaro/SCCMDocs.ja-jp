---
title: "Intune スタンドアロンまたはハイブリッド MDM の選択 | Microsoft Docs"
description: "Intune と Configuration Manager を使用してハイブリッド モバイル デバイス管理を展開するか、Intune スタンドアロンを実行するかを選択します。"
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 648bc6b96aa5ccc834442a962e6d5b5125f88bb5
ms.openlocfilehash: ddb6d47e5dba4fddd6fa811d83b1bf0c91ad26f9
ms.contentlocale: ja-jp
ms.lasthandoff: 07/19/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune によるモバイル デバイス管理 (MDM) について最もよく寄せられる質問の 1 つは、"Intune と Configuration Manager を統合するべきか (ハイブリッド MDM)、クラウドのみの構成で Intune スタンドアロンを実行すべきか" というものです。 この質問に答えるには、2 つのオプションを注意深く比較する必要があります。

## <a name="intune-standalone"></a>Intune スタンドアロン
Intune スタンドアロンは、Microsoft が推奨する展開トポロジです。 Intune スタンドアロンはクラウドのみの MDM ソリューションで、世界中のどこからでもアクセスできる Web コンソールで管理されます。 Intune データセンターは、北米、ヨーロッパ、アジアでホストされています。 Intune はクラウド サービスであるため、比較的短期間でデバイスに Intune 管理を展開できます。

オンプロミスのコンポーネントへの依存関係がないため、スタンドアロン トポロジの方が早く簡単に展開できると感じるお客様は多くおられます。 現在、Intune スタンドアロンは Microsoft Azure クラウド プラットフォームに移行し、次のような高度な機能を数多く提供しています。
- 統合エンタープライズ モビリティ管理プラットフォーム - Intune、Azure AD Premium、Azure Information Protection 向けの Azure Portal での統合されたクラウド プラットフォームおよび管理者エクスペリエンスです。
- モバイル デバイス管理 - モバイル デバイスの豊富な管理機能および情報保護機能です。
- スケーリング - スケーリングの心配をすることなく、モバイル デバイスの展開および管理が可能です。
- ロール ベースのアクセス制御 – 割り当てられた役割やスコープに基づき、管理機能へのアクセスを制限します。
- プログラムによるアクセス (API) – Microsoft Graph API サポート、および SDK と PowerShell の管理オプションです。
- Web コンソール - 最新の Web ブラウザーに対応した、Web 標準を基盤とする HTML 5 ベースのコンソールです。
- 高度なレポート機能 - カスタマイズされたレポートを作成する機能です。
- 機敏性 - 新しい機能を簡単にセットアップし、迅速に配信できます。


## <a name="hybrid-mdm-with-configuration-manager"></a>Configuration Manager とのハイブリッド MDM
ハイブリッド MDM は、Intune のモバイル デバイス管理機能を Configuration Manager に統合するソリューションです。 ポリシー、プロファイル、アプリケーションをデバイスに配信するためのチャネルとして Intune を利用し、Configuration Manager のオンプレミス インフラストラクチャを使用してコンテンツとデバイスを管理します。 ハイブリッドを導入すると、“1 枚のガラス窓” から制御できます。  これはつまり、同じオンプレミス インフラストラクチャと管理コンソールを利用して、Intune でモバイル デバイスを管理しつつ、従来の Configuration Manager クライアントで PC やサーバーを管理できるということです。 ハイブリッド MDM を選択する理由には、次のようなものが挙げられます。  
- Intune に登録されているモバイル デバイスと、Configuration Manager クライアントで管理しているデバイスの両方を、同じ管理コンソールから管理したい
- ご利用のインフラストラクチャで、モバイル デバイスへの証明書の配信に複数の NDES サーバーが必要
- ご利用のインフラストラクチャで、複数の Exchange コネクタが必要
- S/MIME 暗号化サポートが必要


## <a name="changing-the-mdm-authority-setting"></a>MDM 機関の設定変更
MDM 機関の設定を変更する必要がある場合は、Microsoft サポートに連絡しなくても、また、既存の管理対象デバイスの登録を解除して再登録しなくても、お客様自身で変更できます。 詳細については、「[MDM 機関を変更する](/sccm/mdm/deploy-use/change-mdm-authority.md)」を参照してください。

> [!NOTE]    
> MDM 機関を Intune スタンドアロンに変更するには、1610 以降のバージョンの Configuration Manager が必要です。 それより古いバージョンの Configuration Manager をお持ちの場合、MDM 機関の変更は可能ですが、Microsoft サポートによる支援や操作が必要です。 また、MDM 機関の変更後にすべてのデバイスの登録を解除して再登録する必要もあります。  

