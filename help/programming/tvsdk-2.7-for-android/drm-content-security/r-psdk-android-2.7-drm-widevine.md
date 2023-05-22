---
description: 您可以將Android本機Widevine DRM與DASH流一起使用。
title: 維德文DRM
exl-id: 6a011cd7-446a-4f3a-ae36-110618001bf3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# 維德文DRM {#widevine-drm}

您可以將Android本機Widevine DRM與DASH流一起使用。

呼叫以下 `com.adobe.mediacore.drm.DRMManager` 開始播放前的API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

參數：

* `drm` - `"com.widevine.alpha"` 維迪文的。

* `licenseServerURL`  — 接收許可證請求的WideVine許可證伺服器的URL。
* `requestProperties`  — 包含要包括在傳出許可證請求中的額外標頭。

例如，在使用為Expressplay DRM打包的內容時，在播放前使用以下代碼：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
