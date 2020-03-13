---
description: 您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商的DRM解決方案，做為Adobe整合解決方案的替代方案。
seo-description: 您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商的DRM解決方案，做為Adobe整合解決方案的替代方案。
seo-title: Widevine DRM
title: Widevine DRM
uuid: 3a5fd786-4319-4e92-83b6-0f5328df6a44
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Widevine DRM {#widevine-drm}

您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商的DRM解決方案，做為Adobe整合解決方案的替代方案。

如需協力廠商DRM解決方案可用性的最新資訊，請連絡您的Adobe代表。

<!--<a id="section_1385440013EF4A9AA45B6AC98919E662"></a>-->

您可以搭配DASH串流使用Android原生Widevine DRM。

開始播放前，請 `com.adobe.mediacore.drm.DRMManager` 呼叫下列API:

```java
public static void setProtectionData( 
    String drm,  
    String licenseServerURL,   
    Map<String, String> requestProperties)
```

引數：

* `drm` - `"com.widevine.alpha"` 為Widevine。

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
