---
description: 機會檢測器是TVADK元件，它檢測流中的自定義標籤並識別放置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
title: 自訂機會偵測器和內容解析器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 概述{#customize-opportunity-detectors-and-content-resolvers-overiew}

機會檢測器是TVADK元件，它檢測流中的自定義標籤並識別放置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。

TVSDK包含預設機會偵測器：

* `SpliceOutOpportunityDetector`，瞭解預設廣告提示
* `AdSignalingModeOpportunityGenerator`，負責根據廣告信令模式建立初始廣告放置商機
* `SpliceOutOpportunityGenerator`，負責從任何#EXT-X-CUE標籤建立廣告放置商機

TVSDK也包含預設內容解析程式，可根據播放器項目中的中繼資料索引鍵，提供要插入的內容：

* `AuditudeResolver`，可與Adobe Primetime廣告決策（先前稱為Auditude）伺服器通訊，並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
* Black out content

