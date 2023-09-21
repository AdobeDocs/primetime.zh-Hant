---
title: 更新參考實作資料庫
description: 更新參考實作資料庫
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 更新參考實作資料庫{#update-the-reference-implementation-db}

若要控制許可證發行給指定使用者的使用模式，請將專案新增至參考實作資料庫。

1. 將專案新增至 `Customer` 表格。

   此 `Customer` 此表格包含用於驗證使用者的使用者名稱和密碼。 它也會指出使用者是否有訂閱（根據以下授權發行的授權）： *訂閱* 使用模式)。

1. 根據下載擁有或視訊隨選使用模式授予使用者存取權。

       將專案新增至&#39;CustomerAuthorization&#39;表格以指定：
   
   * 使用模式
   * 使用者可存取的每個內容區段

如需如何填入每個表格的詳細資訊，請參閱 [!DNL PopulateSampleDB.sql] 指令碼(包含在您的Primetime DRM DVD [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 目錄)。
