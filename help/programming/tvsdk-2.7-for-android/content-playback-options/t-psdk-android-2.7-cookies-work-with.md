---
description: 您可以使用TVSDK在Cookie標頭中傳送任意資料，以進行工作階段管理、閘道存取等。
title: 使用Cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
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

建立 `cookieManager` 並將URI的Cookie新增至CookieStore。

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

更新C++ Cookie時會呼叫MediaPlayerEvent.COOKIES_UPDATED事件。 此cookiesUpdatedEvent具有方法getCookieString()，可傳回Cookie的字串值。

以下是程式碼片段的範例：

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```
