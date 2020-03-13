---
description: 代碼可以通過DRMManager請求密鑰。
seo-description: 代碼可以通過DRMManager請求密鑰。
seo-title: HTML5 TVSDK上的主要要求工作流程
title: HTML5 TVSDK上的主要要求工作流程
uuid: a1f50eba-4301-49a1-b2e5-9add6687cff8
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# HTML5 TVSDK上的主要要求工作流程{#key-request-workflow-on-html-tvsdk}

代碼可以通過DRMManager請求密鑰。

瀏覽器TVSDK還通過DRMManager對象公開setProtectionData API:

```
[  /** 
   * This will only work for MSE. 
   * <p> Attach key system specific data to use for DRM 
license acquisition. </p> 
   * @param {Object} protectionData - an object containing property names corresponding to key system name strings 
   * (e.g. "org.w3.clearkey") and associated values being instances of 
   * MediaPlayer.vo.protection.ProtectionData. 
   * @returns {AdobePSDK.PSDKErrorCode} kECSuccess or one of the error codes. 
   * @function 
   * @memberof AdobePSDK.DRMManager# 
   */ 
   setProtectionData: function(protectionData) 
```

您的程式碼必須先呼叫此API，才能以正常方式開始播放內容。 MediaPlayer.vo.protection.ProtectionData記載於下列網址： [https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html](https://vm2.dashif.org/dash.js/docs/jsdocs/MediaPlayer.vo.protection.ProtectionData.html)

以下是PlayReady和Widevine授權伺服器URL的範例保護資料物件。

```
var protectionData = { 
   "com.widevine.alpha": { 
                          "serverURL": "https://wv.service.expressplay.com/hms/wv/rights/ 
                           ?ExpressPlayToken=AQAAABIDKA4AAABQuPPoebWWZZD2l3APRKkkagEDOXm 
                           CjgbhsqJTYeZ9KabkjCvSLvuXGHiVLymBnouGXDdCKpbz5IvB3jCZp9U05pys 
                           l9eavucsWXnA0tafbM-1SSJKXOa70kvxAJ_ybhdcmy7-6g" 
                          }, 
   "com.microsoft.playready": { 
                               "serverURL": "https://expressplay-licensing.axprod.net/ 
                                LicensingService.ashx?ExpressPlayToken=AQAAAw_ZXqcAAAB 
                                gHD1gnn_AMQJKfFCP3k9zbBw2srzBLryJVLXclnjhcSBCz4TBzrtfe 
                                gmSw1hAKdFHTNL-KVBGsI4ygBnfPRBUCvGsVOwpQ944fhq45W06ygJ 
                                roB2xOrM03tbkWcrthI7y_UQdHzufHjcBqKZm8QDoqKpxrxc" 
                               } 
   };
```

TVSDK不提供任何API來強制特定DRM系統，因為每個瀏覽器僅支援一個DRM系統。
