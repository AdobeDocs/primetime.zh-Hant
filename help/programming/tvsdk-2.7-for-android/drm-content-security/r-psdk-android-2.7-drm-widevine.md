---
description: 您可以搭配DASH串流使用Android原生Widevine DRM。
title: Widevine DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Widevine DRM {#widevine-drm}

您可以搭配DASH串流使用Android原生Widevine DRM。

呼叫下列專案 `com.adobe.mediacore.drm.DRMManager` 開始播放前的API：

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

引數：

* `drm` - `"com.widevine.alpha"` 給Widevine。

* `licenseServerURL`  — 接收授權要求的Widevine授權伺服器URL。
* `requestProperties`  — 包含要包含在傳出授權請求中的額外標頭。

例如，使用封裝為Expressplay DRM的內容時，在播放之前請使用下列程式碼：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```
