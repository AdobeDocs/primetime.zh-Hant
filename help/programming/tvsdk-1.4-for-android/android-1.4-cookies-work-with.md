---
description: 您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。
title: 使用Cookie
exl-id: 7482777a-c338-4e0d-b123-ce2712657b8d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。

向金鑰伺服器提出請求時，以下是驗證型別的範例：

1. 您的客戶在瀏覽器中登入您的網站，其登入顯示他們有權檢視內容。
1. 您的應用程式會根據授權伺服器的預期產生驗證Token。 將該值傳遞至TVSDK。
1. TVSDK會在Cookie標頭中設定該值。
1. 當TVSDK請求金鑰伺服器取得金鑰以解密內容時，該請求在Cookie標頭中包含驗證值，因此金鑰伺服器知道該請求有效。

若要使用Cookie：

1. 建立 `cookieManager` 並將URI的Cookie新增至 `cookieStore`.

   例如：

   >[!IMPORTANT]
   >
   >啟用302重新導向時，廣告請求可能會被重新導向到與Cookie所屬網域不同的網域。

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK會在執行階段查詢此CookieManager，檢查是否有任何Cookie與URL相關聯，並自動使用這些專案。

   另一個選項是使用 `cookieHeaders` 在 `NetworkConfiguration` 以設定用於請求的任意Cookie標頭字串。 根據預設，此Cookie標頭只會隨關鍵要求傳送。 若要傳送包含所有請求的Cookie標頭，請使用 `NetworkConfiguration` 方法 `setUseCookieHeadersForAllRequests`：

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
