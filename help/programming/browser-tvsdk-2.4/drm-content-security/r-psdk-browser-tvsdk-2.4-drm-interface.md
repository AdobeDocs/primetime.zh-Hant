---
description: 瀏覽器TVSDK提供DRM介面，可供您用來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。
title: DRM介面概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# DRM介面概述{#drm-interface-overview}

瀏覽器TVSDK提供DRM介面，可供您用來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM支援適用於受Microsoft PlayReady （在Windows 8.1和Edge上的Internet Explorer上）以及Widevine (在Google Chrome上) DRM系統保護的MPEG-Dash資料流。 DRM支援適用於Safari上受FairPlay保護的HLS資料流。

DRM工作流程的主要介面為 `DRMManager`. 對的參照 `DRMManager` 可以透過MediaPlayer例項取得例項：

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

以下是播放DRM保護內容的高階工作流程：

1. 若要附加瀏覽器TVSDK在受保護資料流的授權贏取程式中將會使用的DRM系統特定資料，請在叫用前進行下列呼叫 `mediaPlayer.replaceCurrentResource`：

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

1. 如果相同的內容預期可在不同的瀏覽器中搭配不同的DRM系統使用，則可以為多個DRM系統指定保護資料。

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

1. 如果未設定保護資料，則會從DRM系統的PSSH方塊中擷取必要資訊（例如許可證URL）。

   >[!TIP]
   >
   >指定保護資料會覆寫PSSH方塊中指定的授權URL。

1. 依照預設，DRM許可證的作業階段型別是暫時的，這表示在作業階段關閉後不會儲存許可證。

   您可以在以下位置使用API指定工作階段型別： `DRMManager`.  為了回溯相容性，階段作業型別包括 `temporary`， `persistent-license`， `persistent-usage-record`、和 `persistent`.

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 當 `sessionType` 已使用的是 `persistent-license` 或 `persistent`，可透過叫用傳回DRM授權 `DRMManager.returnLicense`.

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
