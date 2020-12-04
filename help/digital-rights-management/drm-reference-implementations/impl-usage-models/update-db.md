---
seo-title: 更新參考實作DB
title: 更新參考實作DB
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 更新參考實施DB{#update-the-reference-implementation-db}

要控制向指定用戶頒發許可證的使用模型，請將條目添加到參考實施資料庫。

1. 將條目添加到`Customer`表中。

   `Customer`表格包含用於驗證用戶的用戶名和密碼。 它還指示用戶是否有訂閱（根據&#x200B;*Subscription*&#x200B;使用模式頒發的授權）。

1. 根據「下載至擁有」或「隨選視訊」使用模式授與使用者存取權。

       將項添加到「CustomerAuthorization」表以指定：
   
   * 使用模式
   * 使用者可存取的每個內容區段

有關如何填入每個表格的詳細資訊，請參閱[!DNL PopulateSampleDB.sql]指令碼（包含在[!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]目錄的Primetime DRM DVD中）。
