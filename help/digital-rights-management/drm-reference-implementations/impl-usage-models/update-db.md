---
seo-title: 更新參考實作DB
title: 更新參考實作DB
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 更新參考實作DB{#update-the-reference-implementation-db}

要控制向指定用戶頒發許可證的使用模型，請將條目添加到參考實施資料庫。

1. 將條目添加到表 `Customer` 中。

   該表 `Customer` 包括用於驗證用戶的用戶名和密碼。 它也會指出使用者是否有訂閱(根據「訂閱」使用模式核發的 *授權* )。

1. 根據「下載至擁有」或「隨選視訊」使用模式授與使用者存取權。

       將項添加到「CustomerAuthorization」表以指定：
   
   * 使用模式
   * 使用者可存取的每個內容區段

如需如何填入每個表格的詳細資訊，請參 [!DNL PopulateSampleDB.sql] 閱指令碼(位於目錄中的Primetime DRM DVD中 [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] )。
