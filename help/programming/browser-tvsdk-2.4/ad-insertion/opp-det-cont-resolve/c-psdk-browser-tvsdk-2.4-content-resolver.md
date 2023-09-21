---
description: 機會偵測器是瀏覽器TVSDK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 自訂機會偵測器和內容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 概觀 {#customize-opportunity-detectors-and-content-resolvers-overview}

機會偵測器是瀏覽器TVSDK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。

瀏覽器TVSDK包含下列預設機會偵測器：

* `AdSignalingModeOpportunityGenerator`，會根據廣告訊號模式建立初始廣告刊登商機。
* `ManifestCuesOpportunityGenerator`，會從任何剪接出標籤建立廣告投放商機。

瀏覽器TVSDK也包含預設內容解析器，例如 `AuditudeResolver`，會根據播放器專案中的中繼資料索引鍵提供要插入的內容。 `AuditudeResolver` 能夠與Adobe Primetime ad decisioning伺服器通訊，並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以透過下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
