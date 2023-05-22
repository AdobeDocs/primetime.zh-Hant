---
description: 瀏覽器TVSDK提供預設機會生成器和內容解析器，這些生成器和解析器基於清單中的非標準標籤。 您的應用程式可能需要根據清單中確定的機會更改時間線。
title: 機會生成器和內容解決器
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 機會生成器和內容解決器{#opportunity-generators-and-content-resolvers}

瀏覽器TVSDK提供預設機會生成器和內容解析器，這些生成器和解析器基於清單中的非標準標籤。 您的應用程式可能需要根據清單中確定的機會更改時間線。

安 *`opportunity`* 表示時間線上通常表示廣告投放機會的關注點。 此機會還可以指示可能影響時間線的自定義操作。 安 *`opportunity generator`* 確定時間線中的特定機會（標籤），並通知TVSDK這些機會已標籤。

在時間表中確定機會 `TimedMetata`。 的 `ManifestCuesOpportunityGenerator` 根據 `TimedMetadata` 為每個拼接輸出ad標籤建立的對象(在 `MediaPlayerItemConfig.adTags`)。 的 `AdSignalingModeOpportunityGenerator` 建立基於 `MediaPlayerItem` 類型及其關聯的ad信令模式。

>[!TIP]
>
>如果 `AdvertisingMetadata.livePreroll` 或 `AdvertisingMetadata.preroll` 屬性已設定， `AdSignalingModeOpportunityGenerator` 為即時流生成預滾動機會。

當您的應用程式收到有關機會（標籤）的通知時，您的應用程式可能會通過插入一系列廣告來更改時間線。 預設情況下，瀏覽器TVSDK調用 *`content resolver`* 以實施所需的時間線更改或操作。 您的應用程式可以使用預設的瀏覽器TVSDK播發內容解析程式或註冊其自己的內容解析程式。

您還可以使用 `MediaPlayerItemConfig.adTags` 為預設添加更多廣告標籤標籤/提示 `ManifestCuesOpportunityGenerator` 類和使用 `MediaPlayerItemConfig.subscribedTags` 以便TVSDK可以通知您的應用程式可能包含廣告工作流資訊的其他標籤。

>[!TIP]
>
>預設值 `MediaPlayerItemConfig.adTags` 和 `MediaPlayerItemConfig.subscribeTags` 是 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`。
