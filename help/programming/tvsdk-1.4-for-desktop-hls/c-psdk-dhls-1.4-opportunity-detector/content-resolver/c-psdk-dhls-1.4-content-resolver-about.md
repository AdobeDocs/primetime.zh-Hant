---
description: TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的機會（例如中斷期間的指標）變更時間表。
title: 機會產生器和內容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 機會產生器和內容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的機會（例如中斷期間的指標）變更時間表。

一個 *`opportunity`* 代表時間軸上的興趣點，通常表示廣告刊登商機。 這個機會也可以指出可能影響時間表的自訂操作，例如中斷期間。 一個 *`opportunity generator`* 會識別時間軸中的特定機會（標籤），並通知TVSDK這些機會已標籤。 在的時間表中識別機會 `TimedMetadata`. 此 `SpliceOutOpportunityGenerator` 根據以下專案建立商機： `TimedMetadata` 針對資訊清單中偵測到的每個廣告標籤所建立的物件，以及 `AdSignalingModeOpportunityGenerator` 建立以下基礎之初始商機 `MediaPlayerItem` 型別及其關聯的廣告訊號模式。

當您的應用程式收到有關商機（標籤）的通知時，您的應用程式可能會變更時間表，例如插入一連串廣告、切換至替代資料流（中斷）或編輯時間表內容。 根據預設，TVSDK會呼叫適當的 *`content resolver`* 以實施所需的時間表變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式或註冊自己的內容解析程式。

您也可以使用 `PSDKConfig.adTags` 新增更多預設的廣告標籤標籤/提示 `SpliceOutOpportunityGenerator` 類別與使用 `PSDKConfig.setSubscribedTags` 以便TVSDK可以將可能含有廣告工作流程資訊的其他標籤通知給應用程式。

自訂解析器的一個可能用途是用於中斷期間。 若要處理這些期間，您的應用程式可以實作並註冊負責處理中斷標籤的中斷機會偵測器。 TVSDK遇到此標籤時，會輪詢所有註冊的內容解析器，以尋找第一個處理指定標籤的內容解析器。 在此範例中，這是中斷內容解析程式，可以取代目前專案，在標籤指定的期間內使用播放器上的替代內容。
