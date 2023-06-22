---
description: 瀏覽器TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器會根據資訊清單中的非標準標籤。 您的應用程式可能需要根據資訊清單中識別的機會，變更時間表。
title: 機會產生器和內容解析器
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 機會產生器和內容解析器{#opportunity-generators-and-content-resolvers}

瀏覽器TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器會根據資訊清單中的非標準標籤。 您的應用程式可能需要根據資訊清單中識別的機會，變更時間表。

一個 *`opportunity`* 代表時間軸上的興趣點，通常表示廣告投放機會。 此機會也可以指出可能影響時間表的自訂操作。 一個 *`opportunity generator`* 會識別時間軸中的特定機會（標籤），並通知TVSDK這些機會已標籤。

在的時間表中識別機會 `TimedMetata`. 此 `ManifestCuesOpportunityGenerator` 根據以下專案建立商機： `TimedMetadata` 為每個剪下廣告標籤建立的物件(在 `MediaPlayerItemConfig.adTags`)，此資訊清單中偵測到。 此 `AdSignalingModeOpportunityGenerator` 建立以「 」為基礎的初始商機 `MediaPlayerItem` 型別及其相關聯的廣告訊號模式。

>[!TIP]
>
>如果 `AdvertisingMetadata.livePreroll` 或 `AdvertisingMetadata.preroll` 屬性已設定， `AdSignalingModeOpportunityGenerator` 為即時資料流產生前段機會。

當應用程式收到商機（標籤）通知時，應用程式可能會透過插入一系列廣告等方式變更時間表。 依預設，瀏覽器TVSDK會呼叫適當的 *`content resolver`* 以實作必要的時間表變更或動作。 您的應用程式可以使用預設的瀏覽器TVSDK廣告內容解析程式或註冊自己的內容解析程式。

您也可以使用 `MediaPlayerItemConfig.adTags` 新增更多預設的廣告標籤標籤/提示 `ManifestCuesOpportunityGenerator` 類別與使用 `MediaPlayerItemConfig.subscribedTags` 以便TVSDK可以將可能含有廣告工作流程資訊的其他標籤通知給您的應用程式。

>[!TIP]
>
>預設值 `MediaPlayerItemConfig.adTags` 和 `MediaPlayerItemConfig.subscribeTags` 是 `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
