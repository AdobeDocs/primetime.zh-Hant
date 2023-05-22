---
title: 更新引用實現DB
description: 更新引用實現DB
copied-description: true
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 更新引用實現DB{#update-the-reference-implementation-db}

要控制向指定用戶頒發許可證的使用模型，請向參考實現資料庫添加條目。

1. 將條目添加到 `Customer` 的子菜單。

   的 `Customer` 表包含用於驗證用戶的用戶名和密碼。 它還指示用戶是否具有訂閱(根據 *訂閱* 使用模式)。

1. 根據「Download-to-own（自用）」或「Video-on-demand（視頻點播）」使用模式授予用戶訪問權限。

       將條目添加到「CustomerAuthorization」表以指定：
   
   * 使用模型
   * 用戶可以訪問的每段內容

有關如何填充每個表的詳細資訊，請參閱 [!DNL PopulateSampleDB.sql] 指令碼（包含在您的黃金時段DRM DVD中） [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] )。
