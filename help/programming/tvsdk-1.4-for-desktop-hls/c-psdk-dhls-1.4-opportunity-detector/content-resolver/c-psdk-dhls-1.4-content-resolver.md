---
description: 機會偵測器是TVADK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 自訂機會偵測器和內容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概觀 {#customize-opportunity-detectors-and-content-resolvers-overiew}

機會偵測器是TVADK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。

TVSDK包含預設的商機偵測器：

* `SpliceOutOpportunityDetector`，瞭解預設廣告提示
* `AdSignalingModeOpportunityGenerator`，負責根據廣告訊號模式建立初始廣告刊登商機
* `SpliceOutOpportunityGenerator`，負責從任何廣告標籤建立廣#EXT-X-CUE刊登商機

TVSDK也包含預設內容解析器，可提供根據播放器專案中的中繼資料索引鍵插入的內容：

* `AuditudeResolver`，能夠與Adobe Primetime ad decisioning (先前稱為Auditude)伺服器通訊並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以透過下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
* 封鎖內容
