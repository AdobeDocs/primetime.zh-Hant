---
description: 您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合的Mighine DRM解決方案的替代方案。
keywords: DRM;DASH;HLS
title: 黃金時段DRM介面概述
exl-id: e07c1551-5a9b-4907-94ea-6b7536918b91
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 黃金時段DRM介面概述 {#primetime-drm-interface-overview}

您可以使用黃金時段Digital Rights Management(DRM)系統的功能來提供對視頻內容的安全訪問。 或者，您可以使用第三方DRM解決方案作為Adobe整合的Mighine DRM解決方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

請咨詢您的Adobe代表，瞭解有關第三方DRM解決方案可用性的最新資訊。

黃金時段數字版權管理(DRM)系統的關鍵客戶端元素是DRM管理器。

黃金時段DRM提供可擴展的、高效的工作流，以在TVSDK應用程式中實施內容保護。 通過為每個數字媒體檔案建立許可證，您可以保護和管理視頻內容的權限。

TVSDK支援黃金時段DRM整合作為自定義DRM工作流。 這意味著您的應用程式在使用FlashDRManager播放流之前必須實施DRM驗證工作流。 要啟用此功能，MediaPlayer會為您提供DRM管理器進行身份驗證。

請參閱TVSDK包中包含的DRM示例播放器代碼。

以下是使用DRM的最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的引用：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK問題a `PTMediaPlayerItemDRMMetadataChanged` 當DRM元資料更改時通知。 此元資料幾乎用作 `DRMManager` 類。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保護的流是多比特率(MBR)編碼的，則用於變型播放清單的DRM元資料應與在所有比特率流中使用的元資料相同。

>[!TIP]
>
>在iOS應用中引用受DRM保護的資產URL時，查詢字串參數 `?faxs=1` 必須附加到(MBR)設定級M3U8 URL。 例如：

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

的 `faxs=1` 查詢字串參數指示內容受DRM保護，並相應地在iOSTVSDK中觸發DRM解密工作流。 也可以附加 `faxs=1` 在DRM保護的HLS資產URL上標籤，這些URL的目的地是其他平台；在iOS按要求或在其他平台上被視為非運營者。

## 在TSVDK應用程式中實現黃金時段DRM {#implement-primetime-drm-in-a-tsvdk-application}

黃金時段DRM被整合到TVSDK中，這簡化了在TVSDK應用中實現內容保護。

有關使用黃金時段DRM在TVSDK應用程式中實現內容保護的概述和詳細資訊，請參閱：

* [Adobe PrimetimeTVSDK-DRM工作流(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
