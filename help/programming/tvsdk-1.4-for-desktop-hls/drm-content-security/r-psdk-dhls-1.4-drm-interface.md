---
description: 黃金時段數字版權管理(DRM)系統的關鍵客戶端元素是DRM管理器。
title: 黃金時段DRM介面概述
exl-id: 8d6b9416-5d8a-4d1e-b8e6-47c43389f079
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 黃金時段DRM介面概述{#primetime-drm-interface-overview}

黃金時段數字版權管理(DRM)系統的關鍵客戶端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

黃金時段DRM提供可擴展的、高效的工作流，以在TVSDK應用程式中實施內容保護。 通過為每個數字媒體檔案建立許可證，您可以保護和管理視頻內容的權限。

TVSDK支援黃金時段DRM整合作為自定義DRM工作流。 這意味著您的應用程式在使用Flash播放流之前必須實施DRM驗證工作流 `DRMManager`。 要啟用此功能， `MediaPlayer` 為您提供DRM管理器進行驗證。

以下是使用DRM的最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的引用：

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

有關DRM的詳細資訊，請參閱Adobe PrimetimeDRM文檔。
