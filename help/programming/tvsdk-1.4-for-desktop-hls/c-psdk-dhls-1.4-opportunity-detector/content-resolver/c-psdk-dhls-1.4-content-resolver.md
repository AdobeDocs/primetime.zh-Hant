---
description: 機會偵測器是TVADK元件，可偵測串流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 自訂機會偵測器和內容解析器
exl-id: 0721278c-e128-4afc-ae81-4f23c2644859
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概觀 {#customize-opportunity-detectors-and-content-resolvers-overiew}

機會偵測器是TVADK元件，可偵測串流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。

TVSDK包含預設的機會偵測器：

* `SpliceOutOpportunityDetector`，瞭解預設廣告提示
* `AdSignalingModeOpportunityGenerator`，負責根據廣告訊號模式建立初始廣告刊登商機
* `SpliceOutOpportunityGenerator`，負責從任何廣告標籤建立廣#EXT-X-CUE刊登商機

TVSDK也包含預設內容解析器，此解析器會根據播放器專案中的中繼資料索引鍵提供要插入的內容：

* `AuditudeResolver`，能夠與Adobe Primetime ad decisioning （先前稱為Auditude）伺服器通訊並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以透過以下方式自訂廣告工作流程：

* 新增對自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂的廣告提供者
* 封鎖內容
