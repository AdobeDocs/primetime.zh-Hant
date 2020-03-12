---
description: 瀏覽器TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機來變更時間軸。
seo-description: 瀏覽器TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機來變更時間軸。
seo-title: 機會產生器和內容解決器
title: 機會產生器和內容解決器
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 機會產生器和內容解決器{#opportunity-generators-and-content-resolvers}

瀏覽器TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機來變更時間軸。

A *`opportunity`* 代表時間軸上的興趣點，通常表示廣告位置機會。 此業務機會還可以指示可能影響時間軸的自定義操作。 An *`opportunity generator`* designs specific opportunity(tags) in the timeline and notifications TVSDK thathe portunitys have ben tagd.

在中的時間軸中可發現機會 `TimedMetata`。 根據 `ManifestCuesOpportunityGenerator` 為清單中已偵測 `TimedMetadata` 到的每個剪接出廣告標籤(在 `MediaPlayerItemConfig.adTags`)所建立的物件來建立商機。 根 `AdSignalingModeOpportunityGenerator` 據類型及其關聯的廣告信令模式 `MediaPlayerItem` 建立初始機會。

>[!TIP]
>
>如果設 `AdvertisingMetadata.livePreroll` 置或 `AdvertisingMetadata.preroll` 屬性， `AdSignalingModeOpportunityGenerator` 則為即時流生成前段機會。

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會透過例如插入一系列廣告來變更時間軸。 依預設，瀏覽器TVSDK會呼叫適當的 *`content resolver`* 呼叫，以實作所需的時間軸變更或動作。 您的應用程式可以使用預設的瀏覽器TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使 `MediaPlayerItemConfig.adTags` 用新增更多預設類別的廣告標籤標籤／提示， `ManifestCuesOpportunityGenerator` 並使用 `MediaPlayerItemConfig.subscribedTags` ，讓TVSDK可通知您的應用程式其他可能包含廣告工作流程資訊的標籤。

>[!TIP]
>
>和的缺 `MediaPlayerItemConfig.adTags` 省值 `MediaPlayerItemConfig.subscribeTags` 為 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`。

