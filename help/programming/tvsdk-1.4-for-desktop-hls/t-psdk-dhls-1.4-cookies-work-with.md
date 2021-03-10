---
description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
title: 使用Cookie
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '234'
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

1. 使用`NetworkConfiguration`中的`cookieHeaders`屬性來設定Cookie。 `cookieHeaders`屬性是中繼資料物件，您可以新增索引鍵值配對至此物件，以加入Cookie標題中。

   例如：

   ```
   var metadata:Metadata = new Metadata(); 
   metadata.setValue(“val1”, “12345”); 
   metadata.setValue(“val2”, “abcd”); 
   
   networkConfiguration.cookieHeaders = metadata;
   ```

   依預設，Cookie標題只會與關鍵要求一起傳送。 若要傳送包含所有請求的Cookie標頭，請將`NetworkConfiguration`屬性`useCookieHeadersForAllRequests`設為true。

1. 若要確保`NetworkConfiguration`正常運作，請將它設為中繼資料：

   ```
   var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   networkConfiguration.forceNativeNetworking = true; 
   var resourceMetadata:Metadata = new Metadata(); 
   resourceMetadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                                networkConfiguration);
   ```

1. 建立`MediaResource`時，請提供上一步的中繼資料。

   例如，如果您使用`createFromURL`方法，請輸入以下資訊：

   ```
   var resource:MediaResource = MediaResource.createFromURL(url, resourceMetadata);
   ```

