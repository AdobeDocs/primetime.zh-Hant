---
description: 機會生成器通過流中的定製標籤、以及信令模式定制標籤等來識別放置機會。 機會生成器將這些放置機會發送到內容解析器，內容解析器基於放置機會的屬性和元資料定制內容/廣告插入工作流。
title: 定制機會生成器和內容解決器
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 概述 {#customize-opportunity-generators-and-content-resolvers-overview}

機會生成器通過流中的定製標籤、以及信令模式定制標籤等來識別放置機會。 機會生成器將這些放置機會發送到內容解析器，內容解析器基於放置機會的屬性和元資料定制內容/廣告插入工作流。

TVSDK包括以下預設機會生成器：

* `ManifestCuesOpportunityGenerator` 根據預設廣告提示生成機會( `#EXT-X-CUE`)。

* `AdSignalingModeOpportunityGenerator` 為指定的ad信令模式生成初始機會。 這會忽略任何提示或定時元資料資訊。
* `CustomMarkerOpportunityGenerator` 生成替換C3廣告的機會。
* `AuditudeResolver`當懶惰的廣告解決開啟時，「機會生成器」會產生機會。

TVSDK還包括預設內容解析器：

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`它可以與黃金時段廣告決策進行通信。

您可以改寫預設的機會生成器和內容解析器，以通過以下方式自定義廣告工作流：

* 識別廣告插入的自定義標籤。 有關詳細資訊，請參見 [定制機會生成器和內容解決器](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md)。
* 建立自定義廣告提供程式。
* 禁止內容。
