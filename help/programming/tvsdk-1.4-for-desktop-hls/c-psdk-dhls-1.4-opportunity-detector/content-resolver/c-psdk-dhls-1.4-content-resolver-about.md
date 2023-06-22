---
description: TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的機會（例如中斷期間的指標）來變更時間表。
title: 機會產生器和內容解析器
exl-id: 6daf7ff4-10c4-4750-8592-94a2be489473
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 機會產生器和內容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的機會（例如中斷期間的指標）來變更時間表。

一個 *`opportunity`* 代表時間軸上的興趣點，通常表示廣告投放機會。 此機會也可以指出可能影響時間表的自訂操作，例如中斷期間。 一個 *`opportunity generator`* 會識別時間軸中的特定機會（標籤），並通知TVSDK這些機會已標籤。 在的時間表中識別機會 `TimedMetadata`. 此 `SpliceOutOpportunityGenerator` 根據以下專案建立商機： `TimedMetadata` 針對資訊清單中偵測到的每個廣告標籤所建立的物件，以及 `AdSignalingModeOpportunityGenerator` 建立以「 」為基礎的初始商機 `MediaPlayerItem` 型別及其相關聯的廣告訊號模式。

當您的應用程式收到有關商機（標籤）的通知時，您的應用程式可能會變更時間表，例如，透過插入一系列廣告、切換至替代資料流（中斷）或編輯時間表內容。 根據預設，TVSDK會呼叫適當的 *`content resolver`* 以實作必要的時間表變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式或註冊自己的內容解析程式。

您也可以使用 `PSDKConfig.adTags` 新增更多預設的廣告標籤標籤/提示 `SpliceOutOpportunityGenerator` 類別與使用 `PSDKConfig.setSubscribedTags` 以便TVSDK可以將可能包含廣告工作流程資訊的其他標籤通知給您的應用程式。

自訂解析器的一種可能使用方式是中斷期間。 若要處理這些期間，您的應用程式可以實作並註冊負責處理中斷標籤的中斷機會偵測器。 當TVSDK遇到此標籤時，它會輪詢所有註冊的內容解析器，以尋找處理指定標籤的第一個。 在此範例中，它是中斷內容解析程式，舉例來說，它可以用播放器上的替代內容取代目前專案，持續時間由標籤指定。
