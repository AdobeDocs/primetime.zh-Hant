---
description: 用戶端程式碼會將資料傳遞至Android API。
seo-description: 用戶端程式碼會將資料傳遞至Android API。
seo-title: Android PSDK上的索引鍵工作流程
title: Android PSDK上的索引鍵工作流程
uuid: 575163de-0f96-434d-a3ff-7e114caf72de
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Android PSDK{#key-request-workflow-on-android-psdk}上的關鍵要求工作流程

用戶端程式碼會將資料傳遞至Android API。

在Android上，您的用戶端程式碼應使用下列API傳入授權伺服器URL及隨附的授權贏取資料：

```
class DRMManager 
   { 
   ... 
   /* 
   * Set the license server URL and attached request properties that the PSDK should use for the passed in drm type.  
   * 
   * drmType: "com.widevine.alpha" for widevine. "com.microsoft.playready" for playready. 
   * licenseServerURL: self explanatory.  
   * requestProperties: key value pairs to be attached as HTTP headers to all license request sent to the passed in license server URL. Pass in 
   * NULL if none is needed.  
   */ 
   public static void setProtectionData(String drmType, String licenseServerURL,  Map<String, String> requestProperties); 
    }
```

成功呼叫此API後，您的程式碼就可以以一般方式開始內容播放。 如果您使用Expressplay，您可以將Token作為授權伺服器URL的一部分傳遞，或作為請求屬性傳遞，並從授權伺服器URL中移除Token。

有些Android裝置同時支援Widevine和PlayReady。 在這種裝置上，如果內容具有多個DRM標頭，則客戶可能希望強制PSDK使用特定DRM解密內容。 這可在播放前呼叫下列API:

```
class MediaPlayer 
   { 
   ... 
    
   /* 
   * drm: pass in "com.widevine.alpha" for widevine or "com.microsoft.playready" for playready 
   * 
   */ 
   public void setDRMScheme(String drm) throws MediaPlayerException 
   }
```

