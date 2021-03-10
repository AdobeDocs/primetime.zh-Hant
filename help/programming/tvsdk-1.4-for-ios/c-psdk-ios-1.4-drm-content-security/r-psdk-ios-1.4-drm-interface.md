---
description: Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。
title: Primetime DRM介面總覽
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Primetime DRM介面概述{#primetime-drm-interface-overview}

您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，做為Adobe整合Primetime DRM解決方案的替代方案。

請洽詢您的Adobe代表，以取得有關協力廠商DRM解決方案可用性的最新資訊。

Primetime數位版權管理(DRM)系統的主要用戶端元素是DRM管理器。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以針對每個數位媒體檔案建立授權，以保護並管理視訊內容的權利。

TVSDK支援將Primetime DRM整合為自訂DRM工作流程。 這表示您的應用程式必須在使用FlashDRManager播放串流之前，先實作DRM驗證工作流程。 若要啟用此功能，MediaPlayer會提供您DRM管理員進行驗證。

請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 媒體播放器中對實現DRM子系統的DRM管理器對象的參考：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK會在DRM中繼資料變更時發出`PTMediaPlayerItemDRMMetadataChanged`通知。 此元資料幾乎用作`DRMManager`類的所有函式的輸入。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保護的流是多比特率(MBR)編碼的，則用於變型播放清單的DRM元資料應與用於所有比特率流的元資料相同。

>[!TIP]
>
>在iOS應用程式中參考受DRM保護的資產URL時，查詢字串參數`?faxs=1`必須附加至(MBR)設定層級的M3U8 URL。 例如：
>
>
```
>https://your.domain.com/hls/[...]/index.m3u8?faxs=1
>```
>
>該`faxs=1`查詢字串參數指示該內容受DRM保護，並相應地在iOS TVSDK中觸發DRM解密工作流。 您也可以在受DRM保護的HLS資產URL上附加`faxs=1`標籤，這些URL會用於其他平台；在iOS上會視為必要項目，或在其他平台上的播放器中視為非作業項目。

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有關DRM的詳細資訊，請參閱[Adobe PrimetimeDRM文檔](https://help.adobe.com/en_US/primetime/drm)。

## 在TSVDK應用程式{#implement-primetime-drm-in-a-tsvdk-application}中實施Primetime DRM

Primetime DRM已整合至TVSDK，可簡化在TVSDK應用程式中實作內容保護。

如需使用Primetime DRM在TVSDK應用程式中實作內容保護的概觀和詳細資訊，請參閱：

* [Adobe PrimetimeTVSDK-DRM工作流程(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)