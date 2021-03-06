---
title: "ネットワーク共有からの Endpoint Protection のマルウェア定義 | Microsoft Docs"
description: "Configuration Manager で Endpoint Protection のマルウェア定義を Microsoft Update からダウンロードできるようにする方法について説明します。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: bff083fe279cd6b36a58305a5f16051ea241151e
ms.openlocfilehash: 344f551a370378620d3d11870993a77e60f9f685
ms.contentlocale: ja-jp
ms.lasthandoff: 12/16/2016


---

# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Configuration Manager で Endpoint Protection のマルウェア定義を Microsoft Update からダウンロードできるようにする

*適用対象: System Center Configuration Manager (Current Branch)*


 Microsoft Update から定義ファイルの更新を選び、ダウンロードする場合、クライアントは [マルウェア対策ポリシー] ダイアログ ボックスの **[定義ファイルの更新]** セクションで定義した間隔で Microsoft Update サイトをチェックします。

 この方法は、クライアントが Configuration Manager サイトに接続されていない場合、またはユーザーから定義ファイルの更新を開始できるようにする場合に役立ちます。

> [!IMPORTANT]
>  この方法を使用して定義ファイルの更新をダウンロードするには、クライアントがインターネット経由で Microsoft Update にアクセスできなければなりません。

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Microsoft マルウェア プロテクション センターを使用して定義ファイルをダウンロードするには
 Microsoft マルウェア プロテクション センターから、定義ファイルの更新をダウンロードできるようにクライアントを構成することができます。 Endpoint Protection クライアントは、別のソースから更新をダウンロードできない場合に、このオプションを使用して定義ファイルの更新をダウンロードします。 この更新方法は、Configuration Manager インフラストラクチャに更新ファイルの配布を妨げる問題がある場合に役立ちます。

> [!IMPORTANT]
>  この方法を使用して定義ファイルの更新をダウンロードするには、クライアントがインターネット経由で Microsoft Update にアクセスできなければなりません。


> [!div class="button"]
[次のステップ >](endpoint-antimalware-policies.md)

> [!div class="button"]
[戻る >](endpoint-configure-alerts.md)

