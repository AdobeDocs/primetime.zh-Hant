---
description: 機會檢測器是瀏覽器TVSDK元件，它檢測流中的自定義標籤並識別放置機會。 這些機會被發送到內容解析器，內容解析器基於放置機會屬性和元資料定制內容/廣告插入工作流。
title: 自定義機會檢測器和內容解析器
exl-id: 1866ed53-acfc-45d3-941e-0ed171aa038b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 概述 {#customize-opportunity-detectors-and-content-resolvers-overview}

機會檢測器是瀏覽器TVSDK元件，它檢測流中的自定義標籤並識別放置機會。 這些機會被發送到內容解析器，內容解析器基於放置機會屬性和元資料定制內容/廣告插入工作流。

瀏覽器TVSDK包括以下預設機會檢測器：

* `AdSignalingModeOpportunityGenerator`它基於廣告信令模式建立初始廣告投放機會。
* `ManifestCuesOpportunityGenerator`，從任何拼接標籤建立廣告放置機會。

瀏覽器TVSDK還包括預設內容解析器，如 `AuditudeResolver`，提供將基於播放器項中的元資料鍵插入的內容。 `AuditudeResolver` 能夠與Adobe Primetime通信並決定伺服器，並返回要放置的廣告中斷。

您可以覆蓋預設的機會檢測器和內容解析器，以通過以下方式自定義廣告工作流：

* 添加對自定義標籤檢測的支援
* 識別廣告插入的自定義標籤
* 建立自定義廣告提供程式
