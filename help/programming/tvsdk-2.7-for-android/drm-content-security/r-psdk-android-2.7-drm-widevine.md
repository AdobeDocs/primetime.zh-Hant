---
description: 您可以搭配DASH資料流使用Android原生Widevine DRM。
title: Widevine DRM
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以搭配DASH資料流使用Android原生Widevine DRM。

呼叫下列專案 `com.adobe.mediacore.drm.DRMManager` 開始播放前的API：

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

引數：

* `drm` - `"com.widevine.alpha"` 為Widevine。

* `licenseServerURL` - Widevine授權伺服器接收授權要求的URL。
* `requestProperties`  — 包含要包含在傳出授權請求中的額外標頭。

例如，使用封裝為Expressplay DRM的內容時，在播放之前請使用下列程式碼：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
