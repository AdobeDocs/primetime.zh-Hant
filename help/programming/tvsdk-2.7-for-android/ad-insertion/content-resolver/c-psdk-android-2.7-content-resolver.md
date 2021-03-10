---
description: 機會生成器通過流中的自定義標籤、廣告信令模式自定義標籤等來識別放置機會。 機會生成器將這些放置機會發送給內容解析器，內容解析器根據放置機會的屬性和元資料定制內容／廣告插入工作流。
title: 自訂商機產生器和內容解析器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# 概述{#customize-opportunity-generators-and-content-resolvers-overview}

機會生成器通過流中的自定義標籤、廣告信令模式自定義標籤等來識別放置機會。 機會生成器將這些放置機會發送給內容解析器，內容解析器根據放置機會的屬性和元資料定制內容／廣告插入工作流。

TVSDK包含下列預設機會產生器：

* `ManifestCuesOpportunityGenerator` 從預設廣告提示( `#EXT-X-CUE`)產生機會。

* `AdSignalingModeOpportunityGenerator` 為指定的廣告信令模式生成初始機會。這會忽略任何提示或計時中繼資料資訊。
* `CustomMarkerOpportunityGenerator` 產生取代C3廣告的機會。
* `AuditudeResolver`當懶惰的廣告解析開啟時，機會產生器會產生機會。

TVSDK也包含預設內容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`，可與Primetime廣告決策通訊。

您可以覆蓋預設的業務機會生成器和內容解析器，以如下方式自定義廣告工作流：

* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者。
* 將內容塗黑。