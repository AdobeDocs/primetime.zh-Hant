---
description: 可以使用TVSDK在Cookie標頭中發送任意資料，用於會話管理、門訪問等。
title: 使用Cookie
exl-id: ea9d83f9-a047-4e24-98e5-f565b8a31a89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
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

建立 `cookieManager` 並將URI的Cookie添加到cookieStore。

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

更新C++ Cookie時調用事件MediaPlayerEvent.COOKIE_UPDATED。 此cookieUpdatedEvent具有為cookie返回字串值的getCookieString()方法。

下面是示例代碼段：

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
