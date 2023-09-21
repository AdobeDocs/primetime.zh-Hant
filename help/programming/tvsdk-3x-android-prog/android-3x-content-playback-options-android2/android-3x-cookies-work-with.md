---
description: 您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。
title: 使用Cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 使用Cookie {#work-with-cookies}

您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。

以下是傳送給金鑰伺服器的範例要求，其中包含一些驗證：

1. 您的客戶使用瀏覽器登入您的網站，其登入顯示允許此客戶檢視內容。
1. 您的應用程式會根據授權伺服器的預期，產生驗證Token。

   此值會傳遞至TVSDK。
1. TVSDK會在Cookie標頭中設定此值。
1. 當TVSDK向金鑰伺服器提出要求，要求取得金鑰以解密內容時，要求會在Cookie標頭中包含驗證值。

   金鑰伺服器知道要求有效。

若要使用Cookie：

1. 建立 `cookieManager` 並將URI的Cookie新增至CookieStore。

   例如：

   ```java
   CookieManager cookieManager=new CookieManager(); 
   CookieHandler.setDefault(cookieManager);  
   HttpCookie cookie=new HttpCookie("lang","fr"); 
   cookie.setDomain("twitter.com");  
   cookie.setPath("/"); 
   cookie.setVersion(0); 
   cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
   ```

   >[!TIP]
   >
   >當啟用302重新導向時，廣告請求可能會重新導向到與Cookie所屬網域不同的網域。

   TVSDK查詢此專案 `cookieManager` 在執行階段中，檢查是否有任何Cookie與URL相關聯，並自動使用這些Cookie。

   如果在播放期間需要更新應用程式中的Cookie，請勿使用 `networkConfiguration.setCookieHeaders` 作為更新的API將出現在JAVA Cookie存放區中。

   `networkConfiguration.setCookieHeaders` API會為TVSDK的C++ CookieStore設定Cookie。

   使用JAVA Cookie並在應用程式和TVSDK之間共用時，請使用JAVA CookieStore來單獨管理Cookie。

   在初始化播放之前，使用Cookie管理員將Cookie設定為CookieStore，如上所述。

   TVSDK會自動擷取儲存在CookieStore中的Cookie。

   如果稍後在播放期間需要更新Cookie值，請使用相同的索引鍵和新的值欄位呼叫CookieStore的相同新增方法。

   也設定
   `networkConfiguration.setReadSetCookieHeader`(false)之後再呼叫
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >將此「setReadSetCookieHeader」設定為false後，請使用JAVA Cookie管理員設定主要要求的Cookie。

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
每當C++ Cookie （來自http回應的Cookie）中有更新時，就會觸發此回呼API。 應用程式需要接聽此回呼，並可據此更新其JAVA CookieStore，以便其JAVA中的網路呼叫能夠利用Cookie，如下所示：

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
