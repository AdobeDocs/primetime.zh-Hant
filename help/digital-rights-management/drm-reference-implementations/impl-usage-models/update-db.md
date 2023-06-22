---
title: 更新參考實作DB
description: 更新參考實作DB
copied-description: true
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 更新參考實作DB{#update-the-reference-implementation-db}

若要控制許可證發行給指定使用者的使用模式，請將專案新增至參考實作資料庫。

1. 將專案新增至 `Customer` 表格。

   此 `Customer` 表格包含驗證使用者的使用者名稱和密碼。 它也會指出使用者是否有訂閱(根據以下授權發行的授權： *訂閱* 使用模式)。

1. 根據「下載後擁有」或「視訊隨選」使用模式，授予使用者存取權。

       將專案新增至&#39;CustomerAuthorization&#39;表格以指定：
   
   * 使用模式
   * 使用者可存取的每個內容區段

如需如何填入每個表格的詳細資訊，請參閱 [!DNL PopulateSampleDB.sql] 指令碼(包含在您的Primetime DRM DVD [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 目錄)。
