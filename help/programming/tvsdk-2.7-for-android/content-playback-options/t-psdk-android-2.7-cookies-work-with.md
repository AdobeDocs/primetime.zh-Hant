---
description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-description: 您可以使用TVSDK在Cookie標題中傳送任意資料，以進行作業管理、閘道存取等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: a3b966fd-1263-458d-8303-b4e898372ee1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '258'
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

建立`cookieManager`，並將URI的Cookie新增至CookieStore。

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

更新C++ Cookie時，會呼叫事件MediaPlayerEvent.COOKIES_UPDATED。 此cookiesUpdatedEvent有一個方法getCookieString()，可傳回Cookie的字串值。

范常式式碼片段如下：

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

