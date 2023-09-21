---
description: 使用者端代碼會將資料傳遞至Android API。
title: Android PSDK上的重要請求工作流程
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Android PSDK上的重要請求工作流程{#key-request-workflow-on-android-psdk}

使用者端代碼會將資料傳遞至Android API。

在Android上，您的使用者端代碼應使用下列API傳入授權伺服器URL和隨附的授權贏取資料：

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

成功呼叫此API後，您的程式碼就可以照常開始播放內容。 如果您使用Expressplay，您可以將權杖當作授權伺服器URL的一部分或作為請求屬性傳遞，並從授權伺服器URL中移除權杖。

部分Android裝置同時支援Widevine和PlayReady。 在這類裝置上，如果內容有多個DRM標題，客戶可能會想要強制PSDK使用特定DRM解密內容。 您可以透過在播放前呼叫下列API來達成此目的：

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
