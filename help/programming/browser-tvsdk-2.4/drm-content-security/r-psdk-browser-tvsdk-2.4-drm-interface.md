---
description: 瀏覽器TVSDK提供DRM介面，您可以使用該介面來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。
title: DRM介面概述
exl-id: aa13f042-4472-4fc3-b7ba-61746b8e024a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# DRM介面概述{#drm-interface-overview}

瀏覽器TVSDK提供DRM介面，您可以使用該介面來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM支援可用於使用MicrosoftPlayReady（在Windows 8.1和Edge上的Internet Explorer）和Widevine(在GoogleChrome上)DRM系統保護的MPEG-Dash流。 DRM支援適用於受FairPlay保護的Safari上的HLS流。

DRM工作流的關鍵介面是 `DRMManager`。 引用 `DRMManager` 可以通過MediaPlayer實例獲取實例：

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

下面是用於播放受DRM保護的內容的高級工作流：

1. 要附加瀏覽器TVSDK在受保護流的許可證獲取過程中將使用的DRM系統特定資料，請在調用前進行以下調用 `mediaPlayer.replaceCurrentResource`:

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
          "serverURL": { 
             "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
             "license-request": "https://example.com:8096/flashaccess/req", 
             "license-release": "https://example.com:8096/flashaccess/req" 
          }, 
          "httpRequestHeaders": { 
          } 
       } 
   }; 
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 如果期望同一內容在不同的瀏覽器中與不同的DRM系統一起使用，則可為多個DRM系統指定保護資料。

   ```js
   var protectionData = { 
       "com.adobe.primetime": { 
           "serverURL": { 
               "individualization-request": "https://individualization.adobe.com/flashaccess/i15n/v5", 
               "license-request": "https://example.com:8096/flashaccess/req", 
               "license-release": "https://example.com:8096/flashaccess/req" 
           }, 
           "httpRequestHeaders": { 
           } 
       }, 
       "com.widevine.alpha": { 
           "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "dt-custom-data": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.microsoft.playready": { 
           "serverURL": "https://pr.test.expressplay.com/playready/RightsManager.asmx?ExpressPlayToken=<token value>", 
           "httpRequestHeaders": { 
               "http-header-CustomData": "eyJ1c2VySWQiOiIxMjM0NS" 
           } 
       }, 
       "com.apple.fps.1_0": { 
           "serverURL": "https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<token value>", 
           "certificateURL": "Path_To_certificate.cer", 
           "licenseResponseType": "arraybuffer", 
           "httpRequestHeaders": { 
               "Content-type": "application/octet-stream" 
           } 
       }, 
       "org.w3.clearkey": { 
           "clearkeys": { 
               "H3JbV93QV3mPNBKQON2UtQ": "ClKhDPHMtCouEx1vLGsJsA", 
               "IAAAACAAIAAgACAAAAAAAg": "5t1CjnbMFURBou087OSj2w" 
           } 
       } 
   }; 
   
   var drmManager = mediaPlayer.drmManager; 
   drmManager.setProtectionData(protectionData);
   ```

1. 當未設定保護資料時，從DRM系統的PSSH框中檢索必要資訊（如許可證URL）（如果適用）。

   >[!TIP]
   >
   >指定保護資料會覆蓋在PSSH框中指定的許可證URL。

1. 預設情況下，DRM許可證的會話類型是臨時的，這意味著會話關閉後不會儲存許可證。

   可以使用中的API指定會話類型 `DRMManager`。  為了向後相容，會話類型包括 `temporary`。 `persistent-license`。 `persistent-usage-record`, `persistent`。

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 當 `sessionType` 已使用 `persistent-license` 或 `persistent`，可通過調用DRM許可證來返回 `DRMManager.returnLicense`。

   ```js
   var onLicenseReturnFunc = function () { 
       console.log("DRM: License Return Complete "); 
   }, 
   
   onLicenseReturnErrorFunc = function (major, minor, errorString/*, errorServerUrl*/) { 
      console.log("DRM: License Return Error: " + errorString); 
   }, 
   
   drmManager = mediaPlayer.drmManager; 
   
   if (drmManager) { 
       var returnLicenseListener = new  
           AdobePSDK.DRMReturnLicenseListener(onLicenseReturnFunc, onLicenseReturnErrorFunc); 
       drmManager.returnLicense(null, null, null, false, returnLicenseListener, drmLicense.session); 
   }
   ```
