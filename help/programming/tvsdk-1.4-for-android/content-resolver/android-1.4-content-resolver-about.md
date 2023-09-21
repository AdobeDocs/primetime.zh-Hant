---
description: 機會偵測器是TVSDK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。
title: 機會產生器和內容解析器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 機會產生器和內容解析器 {#opportunity-generators-and-content-resolvers}

機會偵測器是TVSDK元件，可偵測資料流中的自訂標籤並識別放置機會。 這些機會會傳送給內容解析器，後者會根據版位機會屬性和中繼資料來自訂內容/廣告插入工作流程。

TVSDK包含預設機會偵測器：

* `SpliceOutPlacementOpportunityDetector`，瞭解預設廣告提示

TVSDK也包含預設內容解析器，這些解析器會根據播放器專案中的中繼資料索引鍵提供要插入的內容：

* `AuditudeResolver` 的 `AUDITUDE_METADATA_KEY`，能夠與Adobe Primetime ad decisioning (先前稱為Auditude)伺服器通訊並傳回要放置的廣告插播。

* `MetadataResolver` 的 `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` 的 `TIME_RANGES_METADATA_KEY`

您可以覆寫預設的機會偵測器和內容解析器，以透過下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
* 封鎖內容

TVSDK提供在時間軸中放置廣告的預設機會產生器和內容解析器，這些產生器和解析器以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的機會（例如中斷期間的指標）變更時間表。

一個 *`opportunity`* 代表時間軸上的興趣點，通常表示廣告刊登商機。 這個機會也可以指出可能影響時間表的自訂操作，例如中斷期間。 一個 *`opportunity generator`* 會識別時間軸中的特定機會（標籤），並通知TVSDK這些機會已標籤。 透過包含非標準（非HLS）標籤，可在中的時間軸中識別商機。

當您的應用程式收到有關商機（標籤）的通知時，您的應用程式可能會變更時間表，例如插入一連串廣告、切換至替代資料流（中斷）或編輯時間表內容。 根據預設，TVSDK會呼叫適當的 *`content resolver`* 以實施所需的時間表變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式或註冊自己的內容解析程式。

您也可以使用 `MediaPlayerItemConfig.setAdTags` 以新增更多廣告標籤標籤/提示，讓TVSDK能夠辨識並使用 `MediaPlayerItemConfig.subscribedTags` 並通知您的應用程式有關可能含有廣告工作流程資訊的其他標籤。

自訂解析器的一個可能用途是用於中斷期間。 若要處理這些期間，您的應用程式可以實作並註冊負責處理中斷標籤的中斷機會偵測器。 TVSDK遇到此標籤時，會輪詢所有註冊的內容解析器，以尋找第一個處理指定標籤的內容解析器。 在此範例中，這是中斷內容解析程式，可以取代目前專案，在標籤指定的期間內使用播放器上的替代內容。
