---
description: 可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。
title: 使用Cookie
exl-id: 7f0e7d77-0718-4df7-8380-0e9351f588bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 使用Cookie {#work-with-cookies}

可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。

下面是對密鑰伺服器的示例請求，其中包含一些身份驗證：

1. 您的客戶在瀏覽器中登錄到您的網站，其登錄資訊顯示允許此客戶查看內容。
1. 根據許可證伺服器預期的內容，您的應用程式生成一個驗證令牌。

   此值將傳遞給TVSDK。
1. TVSDK在cookie標頭中設定此值。
1. 當TVSDK向密鑰伺服器請求獲取密鑰以解密內容時，該請求在cookie頭中包含驗證值。

   密鑰伺服器知道該請求有效。

要使用Cookie，請執行以下操作：

1. 建立 `cookieManager` 並將URI的Cookie添加到cookieStore。

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
   >當啟用302重定向時，可以將廣告請求重定向到不同於cookie所屬的域的域。

   TVSDK查詢此 `cookieManager` 在運行時，檢查是否存在與URL關聯的Cookie，並自動使用這些Cookie。

   如果在播放期間需要在應用程式中更新Cookie，請不要使用 `networkConfiguration.setCookieHeaders` API，因為更新將在JAVA Cookie儲存中發生。

   `networkConfiguration.setCookieHeaders` API將cookie設定為TVSDK的C++ CookieStore。

   當使用JAVA Cookie並在應用程式和TVSDK之間共用它們時，請使用JAVA CookieStore僅管理Cookie。

   在初始化播放之前，使用Cookie管理器將cookie設定為CookieStore，如上所述。

   TVSDK將自動提取CookieStore中儲存的Cookie。

   如果在稍後回放期間需要更新Cookie值，請使用相同的鍵和新值欄位調用CookieStore的相同添加方法。

   也設定
   `networkConfiguration.setReadSetCookieHeader`調用前(false)
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >將此&#39;setReadSetCookieHeader&#39;設定為false後，使用JAVA cookie管理器為密鑰請求設定cookie。

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
只要C++ Cookie中有更新（來自http響應的cookie），將觸發此回調API。 應用程式需要偵聽此回調，並可以相應更新其JAVA CookieStore，以便其JAVA中的網路調用可以使用以下Cookie:

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
