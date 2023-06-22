---
description: 您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。
title: 使用Cookie
exl-id: f7a64c77-7db6-4bae-b299-69267fedc673
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '234'
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

1. 使用 `cookieHeaders` 中的屬性 `NetworkConfiguration` 以設定Cookie。 此 `cookieHeaders` 屬性是中繼資料物件，您可以將索引鍵值配對新增至此物件，以包含在Cookie標頭中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   根據預設，Cookie標頭只會隨關鍵要求傳送。 若要傳送包含所有請求的Cookie標頭，請設定 `NetworkConfiguration` 屬性 `useCookieHeadersForAllRequests` 為true。

1. 若要確保 `NetworkConfiguration` 有效，請將其設定為中繼資料：

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 建立時提供上一步驟的中繼資料 `MediaResource`.

   例如，如果您使用 `createFromURL` 方法，輸入下列資訊：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```
