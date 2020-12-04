---
description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: f060b520-ceec-48ca-929f-683566fe6ae7
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---


# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。

以下是向密鑰伺服器發出請求時具有某種類型驗證的示例：

1. 您的客戶使用瀏覽器登入您的網站，而他們的登入顯示他們可以檢視內容。
1. 您的應用程式會根據授權伺服器的需求產生驗證Token。 將該值傳遞至TVSDK。
1. TVSDK會在Cookie標題中設定該值。
1. 當TVSDK向金鑰伺服器要求取得解密內容的金鑰時，該要求會包含Cookie標題中的驗證值，因此金鑰伺服器會知道該要求有效。

若要使用Cookie:

1. 建立`cookieManager`，並將URI的Cookie新增至`cookieStore`。

   例如：

   >[!IMPORTANT]
   >
   >啟用302重新導向後，廣告請求可重新導向至與Cookie所屬網域不同的網域。

   ```java
   CookieManager cookieManager= new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   TVSDK會在執行時期查詢此cookieManager，檢查是否有任何與URL相關的cookie，並自動使用這些cookie。

   另一個選項是使用`NetworkConfiguration`中的`cookieHeaders`來設定要用於請求的任意Cookie標題字串。 依預設，此Cookie標題只會與關鍵要求一起傳送。 若要傳送包含所有請求的Cookie標題，請使用`NetworkConfiguration`方法`setUseCookieHeadersForAllRequests`:

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
