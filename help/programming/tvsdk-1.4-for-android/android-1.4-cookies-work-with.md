---
description: 可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。
title: 使用Cookie
exl-id: 7482777a-c338-4e0d-b123-ce2712657b8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
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

1. 建立 `cookieManager` 將URI的Cookie添加到 `cookieStore`。

   例如：

   >[!IMPORTANT]
   >
   >當啟用302重定向時，可以將廣告請求重定向到不同於cookie所屬的域的域。

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK在運行時查詢此cookieManager，檢查是否有與URL關聯的cookie，並自動使用這些cookie。

   另一個選項是 `cookieHeaders` 在 `NetworkConfiguration` 設定用於請求的任意cookie標頭字串。 預設情況下，此cookie標頭僅與密鑰請求一起發送。 要發送包含所有請求的Cookie標頭，請使用 `NetworkConfiguration` 方法 `setUseCookieHeadersForAllRequests`:

```java
   NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
    
   Metadata cookie = new MetadataNode(); 
   cookie.setValue("reqPayload", “1234567”); 
   networkConfiguration.setCookieHeaders(cookie); 
   networkConfiguration.setUseCookieHeadersForAllRequests( true ); 
    
   // Set NetworkConfiguration as Metadata:                                                                   
   MetadataNode resourceMetadata = new MetadataNode(); 
   resourceMetadata.setNode(DefaultMetadataKeys.NETWORK_CONFIGURATION.getValue(),  
                            networkConfiguration); 
    
   // Call MediaResource.createFromURL to set the metadata: 
   MediaResource resource = MediaResource.createFromURL(url, resourceMetadata); 
   // Load the resource 
   mediaPlayer.replaceCurrentItem(resource);
```
