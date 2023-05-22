---
description: 機會檢測器是TVADK元件，它檢測流中的定製標籤並識別放置機會。 這些機會被發送到內容解析器，內容解析器基於放置機會屬性和元資料定制內容/廣告插入工作流。
title: 自定義機會檢測器和內容解析器
exl-id: 0721278c-e128-4afc-ae81-4f23c2644859
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概述 {#customize-opportunity-detectors-and-content-resolvers-overiew}

機會檢測器是TVADK元件，它檢測流中的定製標籤並識別放置機會。 這些機會被發送到內容解析器，內容解析器基於放置機會屬性和元資料定制內容/廣告插入工作流。

TVSDK包括預設機會檢測器：

* `SpliceOutOpportunityDetector`，瞭解預設的ad提示
* `AdSignalingModeOpportunityGenerator`，負責根據廣告信令模式建立初始廣告投放機會
* `SpliceOutOpportunityGenerator`，負責從任何#EXT-X-CUE標籤建立廣告投放機會

TVSDK還包括預設內容解析器，該解析器根據播放器項中的元資料鍵提供要插入的內容：

* `AuditudeResolver`能夠與Adobe Primetime廣告決策（以前稱為Auditue）伺服器通信，並返回要放置的廣告中斷。

您可以覆蓋預設的機會檢測器和內容解析器，以通過以下方式自定義廣告工作流：

* 添加對自定義標籤檢測的支援
* 識別廣告插入的自定義標籤
* 建立自定義廣告提供程式
* 黑出內容
