---
description: 機會偵測器是瀏覽器TVSDK元件，可偵測串流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 自訂機會偵測器和內容解析器
exl-id: 1866ed53-acfc-45d3-941e-0ed171aa038b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 概觀 {#customize-opportunity-detectors-and-content-resolvers-overview}

機會偵測器是瀏覽器TVSDK元件，可偵測串流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。

瀏覽器TVSDK包含下列預設機會偵測器：

* `AdSignalingModeOpportunityGenerator`，會根據廣告訊號模式建立初始廣告刊登商機。
* `ManifestCuesOpportunityGenerator`，會從任何剪接出去的標籤中建立廣告投放商機。

瀏覽器TVSDK也包含預設內容解析程式，例如 `AuditudeResolver`，會根據播放器專案中的中繼資料索引鍵插入內容。 `AuditudeResolver` 能夠與Adobe Primetime ad decisioning伺服器通訊，並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以透過以下方式自訂廣告工作流程：

* 新增對自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂的廣告提供者
