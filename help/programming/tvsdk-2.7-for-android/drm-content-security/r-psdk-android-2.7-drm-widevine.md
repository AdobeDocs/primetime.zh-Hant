---
description: 您可以搭配DASH串流使用Android原生Widevine DRM。
seo-description: 您可以搭配DASH串流使用Android原生Widevine DRM。
seo-title: Widevine DRM
title: Widevine DRM
uuid: ceb2f18f-9e53-47d6-9d4b-7004ac1d22c9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# Widevine DRM {#widevine-drm}

您可以搭配DASH串流使用Android原生Widevine DRM。

開始播放前，請呼叫下列`com.adobe.mediacore.drm.DRMManager` API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

引數：

* `drm` -  `"com.widevine.alpha"` for Widevine。

* `licenseServerURL` -接收授權要求的Widevine授權伺服器URL。
* `requestProperties` -包含要包含在傳出授權請求中的額外標題。

例如，當使用Expressplay DRM封裝的內容時，請在播放前使用下列程式碼：

```java
DRMManager.setProtectionData( 
  "com.widevine.alpha",  
  "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken= 
<i>token</i>",  
  null); 
```

