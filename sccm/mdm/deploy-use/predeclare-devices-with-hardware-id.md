---
title: "IMEI または iOS シリアル番号によるデバイスの事前宣言 | Microsoft Docs"
description: "IMEI または iOS シリアル番号を持つ会社所有のデバイスの事前宣言"
ms.custom: na
ms.date: 03/24/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 5eed004bd38a567dfdd4e392300be656a7abe3f7
ms.openlocfilehash: c692fad43807e54cecbd7ab60284ea740d60617d
ms.contentlocale: ja-jp
ms.lasthandoff: 05/25/2017

---
# IMEI または iOS シリアル番号を持つデバイスの事前宣言
<a id="predeclare-devices-with-imei-or-ios-serial-numbers" class="xliff"></a>

*適用対象: System Center Configuration Manager (Current Branch)*

会社が所有するデバイスの International station Mobile Equipment Identity (IMEI) 番号または iOS シリアル番号をインポートすることでデバイスを識別できるようになりました。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  インポートされた情報によって登録するデバイスの**所有権**が、デバイスの一覧で**企業**として設定されます。 Intune ライセンスも、サービスにアクセスする各ユーザーに必要です。  

会社所有の iOS デバイスのシリアル番号をアップロードする場合は、企業登録プロファイルとペアにする必要があります。 したがって、デバイスを Apple の DEP (Device Enrollment Program) または Apple Configurator を使用して登録し、会社所有であることを示す必要があります。

## 会社所有のデバイスを事前宣言する方法
<a id="how-to-predeclare-corporate-owned-devices" class="xliff"></a>

1.    Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[概要]** > **[会社が所有しているすべてのデバイス]** > **[事前に宣言されたデバイス]** の順にクリックします。

2.  **[事前に宣言されたデバイスを作成します]** をクリックします。 事前に宣言されたデバイスを作成しますウィザードが開きます。

3.    デバイス情報を追加する方法を選択します。

     -    **IMEI またはシリアル番号と詳細を含む CSV ファイルをアップロードする**

        このオプションでは、**[参照]** をクリックして情報を含む .csv ファイルを指定し、会社所有のデバイスを事前に宣言します。 .csv ファイルの形式は正しく指定する必要があります。 詳細については、「[アップロードする .csv ファイルの形式](#format-for-uploading-csv-files)」を参照してください。

     -    **IMEI またはシリアル番号と詳細を手動で追加する**

        情報を手動で入力するには、IMEI 番号または iOS シリアル番号とデバイスの詳細を入力します。 エラーや警告を修正してから続行してください。

    **[次へ]** をクリックします。

4. .csv ファイルをアップロードした場合、ファイルのインポート結果を確認します。 デバイス番号が確実にインポートされている場合、Configuration Manager はそれらのデバイスと交換の**詳細**を表示します。 詳細を上書きするデバイスを選択します。 デバイスの詳細を変更するには、デバイスの ID またはシリアル番号を再インポートする必要があります。

  手動で番号を入力する場合は、事前宣言するデバイスのフォームに入力します。

  **[次へ]** をクリックして、続行します。

4. 一覧に iOS シリアル番号がある場合は、使用可能なプロファイルの一覧から **[割り当てる登録プロファイル]** を選択し、**[次へ]** をクリックします。

5. **[次へ]** をクリックして詳細情報を確認し、**[次へ]** をもう一度クリックしてデータをアップロードします。

6. **[閉じる]** をクリックして完了します。

## アップロードする .csv ファイルの形式
<a id="format-for-uploading-csv-files" class="xliff"></a>

IMEI または iOS シリアル番号でデバイスを識別するために使用する .csv ファイルは、ガイダンスとしてのみ示される一番上の行を除き、次の形式で作成する必要があります。 各行には、IMEI 番号または iOS シリアル番号のどちらかの ID 番号を含める必要があります。 IOS デバイスの場合は、両方を含めることができます。 IMEI 番号は、Android、iOS、Windows デバイスのものが使用できます。 この表には、サンプル データが含まれます。

| IMEI 番号  | iOS シリアル番号  | OS | 説明 |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | 会社所有の Windows デバイス|
|   | A1B2C3D4E5C6 | IOS |     会社所有の iOS デバイス|
| 223456789012345 | E6D5C4B3A210 |   IOS |     その他の iOS デバイス|
| 323456789012345 |        |   IOS |     3 番目の iOS デバイス|
| 123456789012346 |         |   ANDROID |     会社所有の Android デバイス|

.csv ファイルにヘッダー行を含めないでください。 次に、CSV 形式の同じサンプル データの例を示します。

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

.csv ファイルの各列には、次の値を指定します。

| 列 1 | 列 2 | 列 3 | 列 4 |
|---|---|---|---|
|スペースなしの IMEI 番号 | iOS シリアル番号 | IOS、WINDOWS、または ANDROID | (省略可能) デバイスの詳細 (1,024 文字以内) |

