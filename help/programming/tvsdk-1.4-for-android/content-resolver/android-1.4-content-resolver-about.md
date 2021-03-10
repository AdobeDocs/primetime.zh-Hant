---
description: 機會檢測器是TVSDK元件，可偵測串流中的自訂標籤並識別位置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
title: 機會產生器和內容解決器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# 機會生成器和內容解析器{#opportunity-generators-and-content-resolvers}

機會檢測器是TVSDK元件，可偵測串流中的自訂標籤並識別位置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。

TVSDK包含預設的機會偵測器：

* `SpliceOutPlacementOpportunityDetector`，瞭解預設廣告提示

TVSDK也包含預設內容解析器，可根據播放器項目中的中繼資料索引鍵提供要插入的內容：

* `AuditudeResolver` For  `AUDITUDE_METADATA_KEY`, For, For With Connessing toAdobe Primetime廣告決策（之前稱為Auditude）伺服器， and reguing ad breaks to be place.

* `MetadataResolver` for  `JSON_METADATA_KEY`

* `CustomAdMarkersContentResolver` for  `TIME_RANGES_METADATA_KEY`

您可以覆寫預設的機會偵測器和內容解析器，以下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
* Black out content

TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。

*`opportunity`*&#x200B;代表時間軸上的興趣點，通常表示廣告投放機會。 此機會還可以指示可能影響時間線的自定義操作，如封鎖期。 *`opportunity generator`*&#x200B;會在時間軸中識別特定商機（標籤），並通知TVSDK這些商機已標籤。 在時間軸中通過包括非標準（非HLS）標籤來識別機會。

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會變更時間軸，例如插入一系列廣告、切換至替代串流（封鎖期）或以其他方式編輯時間軸內容。 依預設，TVSDK會呼叫適當的&#x200B;*`content resolver`*，以實作所需的時間軸變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使用`MediaPlayerItemConfig.setAdTags`新增更多廣告標籤標籤標籤／提示，讓TVSDK能夠識別並使用`MediaPlayerItemConfig.subscribedTags`，並通知您的應用程式其他可能包含廣告工作流程資訊的標籤。

自定義解析器的一個可能用途是用於封鎖期。 要處理這些期間，您的應用程式可以實施並註冊一個負責處理封鎖期標籤的封鎖期機會檢測器。 當TVSDK遇到此標籤時，會輪詢所有已註冊的內容解析器，以尋找第一個處理指定標籤的解析器。 在此範例中，它是封鎖內容解析程式，例如，可在標籤所指定的期間內，以播放器上的替代內容取代目前項目。
