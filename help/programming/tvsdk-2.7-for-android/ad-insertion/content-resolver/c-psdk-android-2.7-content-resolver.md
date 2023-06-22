---
description: 機會產生器會依串流中的自訂標籤、廣告訊號模式自訂標籤等識別位置機會。 機會產生器會將這些刊登機會傳送給內容解析器，後者會根據刊登機會的屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 自訂機會產生器和內容解析器
exl-id: 2ce859c4-6bf6-4ec5-82b1-2bc6a2316fd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 概觀 {#customize-opportunity-generators-and-content-resolvers-overview}

機會產生器會依串流中的自訂標籤、廣告訊號模式自訂標籤等識別位置機會。 機會產生器會將這些刊登機會傳送給內容解析器，後者會根據刊登機會的屬性和中繼資料來自訂內容/廣告插入工作流程。

TVSDK包含下列預設機會產生器：

* `ManifestCuesOpportunityGenerator` 從預設廣告提示產生機會( `#EXT-X-CUE`)。

* `AdSignalingModeOpportunityGenerator` 為指定的廣告訊號模式產生初始機會。 這會忽略任何提示或定時中繼資料資訊。
* `CustomMarkerOpportunityGenerator` 會產生機會來取代內建的C3廣告。
* `AuditudeResolver`的opportunity generator會在懶惰的廣告解決開啟時產生機會。

TVSDK也包含預設內容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可與Primetime和決策通訊。

您可以覆寫預設機會產生器和內容解析器，以透過下列方式自訂廣告工作流程：

* 識別廣告插入的自訂標籤
* 建立自訂的廣告提供者。
* 封鎖內容。
