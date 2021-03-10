---
description: 您可以搭配DASH串流使用Android原生Widevine DRM。
title: Widevine DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
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

