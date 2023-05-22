---
description: 可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。
title: 使用Cookie
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 使用Cookie{#work-with-cookies}

可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。

下面是向密鑰伺服器發出請求時具有某種類型身份驗證的示例：

1. 您的客戶在瀏覽器中登錄到您的網站，其登錄資訊顯示允許他們查看內容。
1. 您的應用程式根據許可證伺服器預期的內容生成驗證令牌。 將該值傳遞給TVSDK。
1. TVSDK在cookie標頭中設定該值。
1. 當TVSDK向密鑰伺服器請求獲取密鑰以解密內容時，該請求包含cookie頭中的驗證值，因此密鑰伺服器知道該請求有效。

要使用Cookie，請執行以下操作：

1. 使用 `cookieHeaders` 物業 `NetworkConfiguration` 來設定cookie。 的 `cookieHeaders` 屬性是元資料對象，您可以向此對象添加鍵值對，以將其包含在cookie標頭中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   預設情況下，僅使用密鑰請求發送cookie標頭。 要發送包含所有請求的Cookie標頭，請設定 `NetworkConfiguration` 屬性 `useCookieHeadersForAllRequests` 是真的。

1. 確保 `NetworkConfiguration` 工作，將其設定為元資料。

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 在建立 `MediaResource`。

   例如，如果 `createFromURL` 方法，輸入以下資訊：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
