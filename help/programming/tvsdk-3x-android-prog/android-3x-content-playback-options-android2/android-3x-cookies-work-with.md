---
description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: 5ada8632a7a5e3cb5d795dc42110844244656095
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 使用Cookie {#work-with-cookies}

您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。

以下是對具有某些驗證的密鑰伺服器的示例請求：

1. 您的客戶使用瀏覽器登入您的網站，其登入顯示此客戶可檢視內容。
1. 您的應用程式會根據授權伺服器的需求產生驗證Token。

   此值會傳遞至TVSDK。
1. TVSDK會在Cookie標題中設定此值。
1. 當TVSDK向金鑰伺服器要求取得解密內容的金鑰時，要求會包含Cookie標題中的驗證值。

   密鑰伺服器知道請求有效。

若要使用Cookie:

1. 建立`cookieManager`，並將URI的Cookie新增至CookieStore。

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
   >啟用302重新導向後，廣告請求可重新導向至與Cookie所屬網域不同的網域。

   TVSDK會在執行時期查詢此`cookieManager`，檢查是否有任何與URL相關的Cookie，並自動使用這些Cookie。

   如果在播放期間需要在應用程式中更新Cookie，請勿使用`networkConfiguration.setCookieHeaders` API，因為更新會發生在JAVA Cookie儲存區。

   `networkConfiguration.setCookieHeaders` API會將Cookie設定至TVSDK的C++ CookieStore。

   當使用JAVA Cookie並在應用程式和TVSDK之間共用時，請使用JAVA CookieStore僅管理Cookie。

   在初始化播放之前，請使用Cookie管理器將Cookie設定為CookieStore，如上所述。

   TVSDK會自動擷取儲存在CookieStore中的Cookie。

   如果Cookie值需要在稍後的播放期間更新，請使用相同的金鑰和新值欄位呼叫相同的CookieStore新增方法。

   也設定
   `networkConfiguration.setReadSetCookieHeader`(false)呼叫前
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >將此&#39;setReadSetCookieHeader&#39;設定為false後，請使用JAVA Cookie管理員來設定關鍵要求的Cookie。

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
每當C++ Cookie（來自http回應的Cookie）中有更新時，就會觸發此回呼API。應用程式需要監聽此回呼，並可依此更新其JAVA CookieStore，如此其JAVA網路呼叫就可利用Cookie，如下所示：

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
