---
description: 瀏覽器TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器會根據資訊清單中的非標準標籤。 您的應用程式可能需要根據資訊清單中識別的機會，變更時間表。
title: 機會產生器和內容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 機會產生器和內容解析器{#opportunity-generators-and-content-resolvers}

瀏覽器TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器會根據資訊清單中的非標準標籤。 您的應用程式可能需要根據資訊清單中識別的機會，變更時間表。

一個 *`opportunity`* 代表時間軸上的興趣點，通常表示廣告刊登商機。 這個機會也可以指出可能影響時間表的自訂操作。 一個 *`opportunity generator`* 會識別時間軸中的特定機會（標籤），並通知TVSDK這些機會已標籤。

在的時間表中識別機會 `TimedMetata`. 此 `ManifestCuesOpportunityGenerator` 根據以下專案建立商機： `TimedMetadata` 為每個剪下廣告標籤建立的物件(在 `MediaPlayerItemConfig.adTags`)中，偵測到它。 此 `AdSignalingModeOpportunityGenerator` 建立以下基礎之初始商機 `MediaPlayerItem` 型別及其關聯的廣告訊號模式。

>[!TIP]
>
>如果 `AdvertisingMetadata.livePreroll` 或 `AdvertisingMetadata.preroll` 屬性已設定， `AdSignalingModeOpportunityGenerator` 為即時資料流產生前段機會。

當您的應用程式收到有關商機（標籤）的通知時，您的應用程式可能會變更時間表，例如插入一系列廣告。 依預設，瀏覽器TVSDK會呼叫適當的 *`content resolver`* 以實施所需的時間表變更或動作。 您的應用程式可以使用預設的瀏覽器TVSDK廣告內容解析程式或註冊自己的內容解析程式。

您也可以使用 `MediaPlayerItemConfig.adTags` 新增更多預設的廣告標籤標籤/提示 `ManifestCuesOpportunityGenerator` 類別與使用 `MediaPlayerItemConfig.subscribedTags` 以便TVSDK可以將可能含有廣告工作流程資訊的其他標籤通知給應用程式。

>[!TIP]
>
>預設值 `MediaPlayerItemConfig.adTags` 和 `MediaPlayerItemConfig.subscribeTags` 是 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
