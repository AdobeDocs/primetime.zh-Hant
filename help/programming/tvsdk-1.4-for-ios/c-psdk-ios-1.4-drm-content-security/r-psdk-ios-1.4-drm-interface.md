---
description: Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。
seo-description: Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。
seo-title: Primetime DRM介面總覽
title: Primetime DRM介面總覽
uuid: 3aae7c7a-fd0c-430e-9018-fd72801ab778
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Primetime DRM介面總覽 {#primetime-drm-interface-overview}

您可以使用Primetime數位版權管理(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，做為Adobe整合Primetime DRM解決方案的替代方案。

請洽詢您的Adobe代表，以取得有關協力廠商DRM解決方案可用性的最新資訊。

Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以針對每個數位媒體檔案建立授權，以保護並管理視訊內容的權利。

TVSDK支援將Primetime DRM整合為自訂DRM工作流程。 這表示您的應用程式必須在使用Flash DRManager播放串流之前，先實作DRM驗證工作流程。 若要啟用此功能，MediaPlayer會提供您DRM管理員進行驗證。

請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的參考：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK會在DRM中 `PTMediaPlayerItemDRMMetadataChanged` 繼資料變更時發出通知。 此中繼資料幾乎用作類別所有功能的輸 `DRMManager` 入。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保護的流是多比特率(MBR)編碼的，則用於變型播放清單的DRM元資料應與用於所有比特率流的元資料相同。

>[!TIP]
>
>在iOS應用程式中參考受DRM保護的資產URL時，查詢字串參 `?faxs=1` 數必須附加至(MBR)設定層級的M3U8 URL。 例如：>
>
```>
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```>
>The `faxs=1` query string parameter signals that the content is DRM protected, and triggers the DRM decryption workflow accordingly in the iOS TVSDK. You can also append the `faxs=1` tag on DRM-protected HLS asset URLs that are destined for other platforms; it is observed as required on iOS or treated as a non-op in players on other platforms.



<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

如需DRM的詳細資訊，請參閱 [Adobe Primetime DRM檔案](https://help.adobe.com/en_US/primetime/drm)。

## 在TSVDK應用程式中實作Primetime DRM {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM已整合至TVSDK，可簡化在TVSDK應用程式中實作內容保護。

如需使用Primetime DRM在TVSDK應用程式中實作內容保護的概觀和詳細資訊，請參閱：

* [Adobe Primetime TVSDK-DRM工作流程(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)