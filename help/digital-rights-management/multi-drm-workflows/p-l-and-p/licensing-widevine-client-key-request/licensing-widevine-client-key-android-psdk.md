---
description: 客戶端代碼將資料傳遞給Android API。
title: Android PSDK上的密鑰請求工作流
exl-id: 3ff52c0d-0789-4fe5-bf9d-f03184bad488
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Android PSDK上的密鑰請求工作流{#key-request-workflow-on-android-psdk}

客戶端代碼將資料傳遞給Android API。

在Android上，您的客戶端代碼應使用以下API在許可證伺服器URL和隨附的許可證獲取資料中傳遞：

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

成功調用此API後，您的代碼便可以按通常方式開始內容回放。 如果使用Expressplay，則可以將令牌作為許可證伺服器URL的一部分或作為請求屬性傳遞，並從許可證伺服器URL中刪除令牌。

一些Android設備同時支援Widevine和PlayReady。 在這些設備上，如果內容具有多個DRM報頭，則客戶可能希望強制PSDK使用特定DRM解密內容。 這可以通過在播放前調用以下API來完成：

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
