---
description: Primetime數位版權管理(DRM)系統的關鍵使用者端元素是DRM管理員。
title: Primetime DRM介面概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Primetime DRM介面概述{#primetime-drm-interface-overview}

Primetime數位版權管理(DRM)系統的關鍵使用者端元素是DRM管理員。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以為每個數位媒體檔案建立授權，以保護和管理視訊內容的許可權。

TVSDK支援Primetime DRM整合作為自訂DRM工作流程。 這表示您的應用程式必須先實作DRM驗證工作流程，才能使用Flash播放資料流 `DRMManager`. 若要啟用此功能， `MediaPlayer` 為您提供用於驗證的DRM管理員。

以下是使用DRM時最重要的API元素：

* 在媒體播放器中，對實作DRM子系統的DRM管理員物件的參照：

  ```
  public function get drmManager():DRMManager 
  ```

<!--<a id="section_4204CE2731A44F67A3664AEDE8CCCA47"></a>-->

其他相關API元素：

* [flash.net.drm.DRMManager](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html)
* [flash.net.drm.DRMContentData](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMContentData.html)
* [flash.net.drm.DRMVoucher](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMVoucher.html)
* [flash.net.drm.AuthenticationMethod](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/AuthenticationMethod.html)
* [flash.events.DRMStatusEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMStatusEvent.html)
* [flash.events.DRMErrorEvent](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/events/DRMErrorEvent.html)

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

如需DRM的詳細資訊，請參閱Adobe Primetime DRM檔案。
