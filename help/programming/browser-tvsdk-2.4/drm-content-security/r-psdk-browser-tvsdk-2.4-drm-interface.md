---
description: 瀏覽器TVSDK提供DRM介面，您可用來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。
title: DRM介面總覽
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# DRM介面概述{#drm-interface-overview}

瀏覽器TVSDK提供DRM介面，您可用來播放受不同DRM解決方案（包括FairPlay、PlayReady和Widevine）保護的內容。

<!--<a id="section_59994F2059B245E996E0776214804A0A"></a>-->

>[!IMPORTANT]
>
>DRM支援適用於使用Microsoft PlayReady（在Windows 8.1和Edge的Internet Explorer上）和Widevine（在Google Chrome上）DRM系統保護的MPEG-Dash串流。 DRM支援適用於使用FairPlay保護的Safari上的HLS串流。

DRM工作流的關鍵介面是`DRMManager`。 您可透過MediaPlayer例項取得對`DRMManager`例項的參考：

* `var mediaPlayer = new AdobePSDK.MediaPlayer();`
* `var drmManager = mediaPlayer.drmManager;`

<!--<a id="section_B7E8AD9A4D4F4BD9BA2A67ABC135D6F9"></a>-->

以下是播放受DRM保護內容的高階工作流程：

1. 若要附加瀏覽器TVSDK將在受保護串流的授權取得程式中使用的DRM系統特定資料，請在叫用`mediaPlayer.replaceCurrentResource`前先進行下列呼叫：

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

1. 如果相同的內容需要在不同瀏覽器中用於不同的DRM系統，則可以為多個DRM系統指定保護資料。

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

1. 當未設定保護資料時，從DRM系統的PSSH框（如果適用）中檢索必要資訊（如許可證URL）。

   >[!TIP]
   >
   >指定保護資料會覆寫在PSSH方塊中指定的授權URL。

1. 預設情況下，DRM許可證的會話類型是臨時的，這意味著在會話關閉後不儲存許可證。

   您可以使用`DRMManager`中的API來指定作業類型。  為了向後相容，會話類型包括`temporary`、`persistent-license`、`persistent-usage-record`和`persistent`。

   ```js
   var drmManager = mediaPlayer.drmManager; 
    drmManager.setEMESessionType(“<YOUR_SESSION_TYPE>”); 
   ```

1. 當使用的`sessionType`是`persistent-license`或`persistent`時，可以通過調用`DRMManager.returnLicense`來返回DRM許可證。

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

