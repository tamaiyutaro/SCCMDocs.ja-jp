---
title: "Configuration Manager でのハイブリッド管理のデバイス向けユーザー アフィニティ | Microsoft Docs"
description: "Configuration Manager で管理対象デバイスのユーザー アフィニティを構成します。"
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
caps.latest.revision: 6
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 74dcc0f4e680893db804956615248b7e1230d2b5

---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Configuration Manager でのハイブリッド管理のデバイス向けユーザー アフィニティ

*適用対象: System Center Configuration Manager (Current Branch)*

管理者は企業所有のデバイスのプロファイルを構成するときに、管理対象デバイスに*ユーザー アフィニティ*を設定できるかどうかを指定できます (ユーザー アフィニティはデバイスで特定のユーザーを識別します)。  

##  <a name="a-namebkmkioscpa-managed-devices-with-user-affinity"></a><a name="BKMK_iOSCP"></a> ユーザー アフィニティありの管理対象デバイス  
 **ユーザー アフィニティ**が構成されているデバイスは、会社のポータル アプリをインストールして実行することにより、アプリをダウンロードしてデバイスを管理できるようになります。 デバイスを受け取ったユーザーは、セットアップ アシスタントを完了して会社ポータル アプリをインストールするために、いくつもの追加の手順を完了する必要があります。  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>ユーザー アフィニティありで iOS デバイスを登録するには  

1.  新しいデバイスの電源を初めてオンにしたとき、ユーザーはセットアップ アシスタントを完了するように求められます。 セットアップ中に資格情報の入力を求めるよう登録プロファイルで指定できます。 ユーザーは、Intune のサブスクリプションに関連付けられている資格情報 (つまり一意の個人名または UPN) を使用する必要があります。  

2.  セットアップ中、ユーザーに Apple ID を要求することもできます。 デバイスを会社ポータルにインストールできるように、Apple ID を入力する必要があります。 セットアップの完了後に iOS の **[設定]** メニューから Apple ID を入力することもできます。  

3.  セットアップが完了したら、iOS デバイスは App Store から[会社ポータル アプリ](https://itunes.apple.com/us/app/id719171358) (たとえば、会社ポータル アプリ) をインストールする必要があります。  

4.  これでユーザーは、デバイスを設定するときに使用した UPN で会社ポータルにログインできるようになります。  

5.  ユーザーはログインすると、デバイスを登録するように求められます。 最初の手順は **デバイスを識別する**ことです。 会社に登録されていてエンドユーザーの Intune アカウントに割り当てられている iOS デバイスの一覧が表示されます。 一致するデバイスを選択します。  

     このデバイスがまだ会社に登録されていない場合は、[新しいデバイス] を選択して、標準登録フローを続行します。  

6.  次の画面で、ユーザーは新しいデバイスのシリアルを確認する必要があります。 ユーザーは [シリアル番号を確認] リンクをクリックして、設定アプリを開始して、シリアル番号を確認できます。 ユーザーは、シリアル番号の最後の 4 文字を会社ポータル アプリに入力する必要があります。  

     この手順では、デバイスが Intune に登録されている会社のデバイスであることが確認されます。 デバイスのシリアル番号が一致しない場合は、間違ったデバイスが選択されています。 前の画面に戻り、別のデバイスを選択します。  

7.  シリアル番号の確認後に、会社ポータル アプリは会社ポータル Web サイトにリダイレクトします。ユーザーはそこで登録を完了すると、アプリに戻るように求められます。  

8.  これで登録が完了します。 このデバイスのすべての機能を使用できるようになります。  

##  <a name="a-namebkmknouaa-managed-devices-without-user-affinity"></a><a name="BKMK_noUA"></a> ユーザー アフィニティなしの管理対象デバイス  
 **ユーザー アフィニティなし**で構成されているデバイスは、会社ポータルをサポートしませんので、アプリをインストールしないでください。 会社ポータルは、会社の資格情報を持ち、カスタマイズされた企業リソース (電子メールなど) へのアクセスを必要とするユーザー向けです。 **ユーザー アフィニティなし** で登録されたデバイスは、専用ユーザー サインインのためのデバイスではありません。 キオスク、販売時点管理 (POS)、または共有ユーティリティ デバイスは、ユーザー アフィニティなしで登録されたデバイスの一般的なユース ケースです。 ユーザー アフィニティが必要な場合は、デバイスの登録プロファイルで **[ユーザー アフィニティ]** が選択されていることを確認してから、デバイスを登録します。 デバイスのアフィニティ ステータスを変更するには、デバイスをインベントリから削除してから再登録する必要があります。



<!--HONumber=Dec16_HO3-->

