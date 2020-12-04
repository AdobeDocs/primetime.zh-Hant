---
description: 機會偵測器是瀏覽器TVSDK元件，可偵測串流中的自訂標籤並識別位置商機。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
seo-description: 機會偵測器是瀏覽器TVSDK元件，可偵測串流中的自訂標籤並識別位置商機。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
seo-title: 自訂機會偵測器和內容解析器
title: 自訂機會偵測器和內容解析器
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# 概述{#customize-opportunity-detectors-and-content-resolvers-overview}

機會偵測器是瀏覽器TVSDK元件，可偵測串流中的自訂標籤並識別位置商機。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。

瀏覽器TVSDK包含下列預設機會偵測器：

* `AdSignalingModeOpportunityGenerator`，這會根據廣告信令模式，創造初始廣告放置機會。
* `ManifestCuesOpportunityGenerator`，這會從任何剪接出的標籤中建立廣告放置機會。

瀏覽器TVSDK也包含預設內容解析器，例如`AuditudeResolver`，可根據播放器項目中的中繼資料索引鍵來提供要插入的內容。 `AuditudeResolver` 能夠與Adobe Primetime廣告決策伺服器通訊，並傳回要放置的廣告插播。

您可以覆寫預設的機會偵測器和內容解析器，以下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者

