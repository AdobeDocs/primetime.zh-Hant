---
description: 您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，作為Adobe整合式Primetime DRM解決方案的替代方案。
keywords: DRM；破折號；HLS
title: Primetime DRM介面概觀
exl-id: e07c1551-5a9b-4907-94ea-6b7536918b91
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Primetime DRM介面概觀 {#primetime-drm-interface-overview}

您可以使用PrimetimeDigital Rights Management(DRM)系統的功能，提供對視訊內容的安全存取。 或者，您也可以使用協力廠商DRM解決方案，作為Adobe整合式Primetime DRM解決方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

請洽詢您的Adobe代表，以取得有關第三方DRM解決方案可用性的最新資訊。

Primetime數位版權管理(DRM)系統的關鍵使用者端元素是DRM管理員。

Primetime DRM提供可擴充、有效率的工作流程，以在TVSDK應用程式中實作內容保護。 您可以為每個數位媒體檔案建立授權，藉此保護和管理視訊內容的許可權。

TVSDK支援Primetime DRM整合作為自訂DRM工作流程。 這表示您的應用程式必須先實作DRM驗證工作流程，才能使用FlashDRMManager播放資料流。 若要啟用此功能，MediaPlayer會提供DRM管理員以進行驗證。

請參閱TVSDK套件中包含的DRM範例播放器程式碼。

以下是使用DRM時最重要的API元素：

* 在媒體播放器中對實作DRM子系統的DRM管理員物件的參考：

   ```
   @property (readonly, nonatomic) DRMManager *drmManager
   ```

<!--<a id="section_F986DB1EDD6F44CD8E57419CCA0921E8"></a>-->

TVSDK問題 `PTMediaPlayerItemDRMMetadataChanged` DRM中繼資料變更時通知。 此中繼資料會用作的幾乎所有函式的輸入 `DRMManager` 類別。

<!--<a id="section_223DCF63BAB6438792A85352A79044CC"></a>-->

如果受DRM保護的資料流是多位元速率(MBR)編碼，則用於變體播放清單的DRM中繼資料應與用於所有位元速率資料流的中繼資料相同。

>[!TIP]
>
>在您的iOS應用程式中參照受DRM保護的資產URL時，查詢字串引數 `?faxs=1` 必須附加至(MBR)設定層級M3U8 URL。 例如：

```
https://your.domain.com/hls/[...]/index.m3u8?faxs=1
```

此 `faxs=1` 查詢字串引數會指出內容受到DRM保護，並在iOS TVSDK中相應地觸發DRM解密工作流程。 您也可以附加 `faxs=1` 標籤位於受動態隨機存取機制保護的HLS資產URL上，且目的地為其他平台；系統視需要在iOS上觀察該標籤，或將其視為其他平台上的播放器中的非作業專案。

## 在TSVDK應用程式中實作Primetime DRM {#implement-primetime-drm-in-a-tsvdk-application}

Primetime DRM已整合至TVSDK，這簡化了TVSDK應用程式中實施內容保護的流程。

如需使用Primetime DRM在TVSDK應用程式中實作內容保護的概述和詳細資訊，請參閱：

* [Adobe Primetime TVSDK-DRM工作流程(PDF)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_tvsdk_drm_workflow.pdf)
