---
description: 瀏覽器TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機來變更時間軸。
title: 機會產生器和內容解決器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# 機會生成器和內容解析器{#opportunity-generators-and-content-resolvers}

瀏覽器TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機來變更時間軸。

*`opportunity`*&#x200B;代表時間軸上的興趣點，通常表示廣告投放機會。 此業務機會還可以指示可能影響時間軸的自定義操作。 *`opportunity generator`*&#x200B;會在時間軸中識別特定商機（標籤），並通知TVSDK這些商機已標籤。

在`TimedMetata`的時間軸中識別機會。 `ManifestCuesOpportunityGenerator`根據為清單中檢測到的每個剪接出廣告標籤（在`MediaPlayerItemConfig.adTags`中）建立的`TimedMetadata`對象建立機會。 `AdSignalingModeOpportunityGenerator`建立基於`MediaPlayerItem`類型及其關聯的廣告信令模式的初始機會。

>[!TIP]
>
>如果設定了`AdvertisingMetadata.livePreroll`或`AdvertisingMetadata.preroll`屬性， `AdSignalingModeOpportunityGenerator`將為即時流生成滾動前機會。

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會透過例如插入一系列廣告來變更時間軸。 依預設，瀏覽器TVSDK會呼叫適當的&#x200B;*`content resolver`*，以實作必要的時間軸變更或動作。 您的應用程式可以使用預設的瀏覽器TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使用`MediaPlayerItemConfig.adTags`新增更多預設`ManifestCuesOpportunityGenerator`類別的廣告標籤標籤／提示，並使用`MediaPlayerItemConfig.subscribedTags`，讓TVSDK通知您的應用程式其他可能包含廣告工作流程資訊的標籤。

>[!TIP]
>
>`MediaPlayerItemConfig.adTags`和`MediaPlayerItemConfig.subscribeTags`的預設值為`[MediaPlayerItemConfig.DEFAULT_AD_TAG]`。

