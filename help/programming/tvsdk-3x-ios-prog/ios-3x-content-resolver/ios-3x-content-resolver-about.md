---
description: 機會檢測器是TVSDK元件，可偵測串流中的自訂標籤並識別位置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
seo-description: 機會檢測器是TVSDK元件，可偵測串流中的自訂標籤並識別位置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。
seo-title: 機會產生器和內容解決器
title: 機會產生器和內容解決器
uuid: c49494da-2145-40d7-8f4b-2ecaf2866ca4
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 機會產生器和內容解決器 {#opportunity-generators-and-content-resolvers}

機會檢測器是TVSDK元件，可偵測串流中的自訂標籤並識別位置機會。 這些機會會傳送至內容解析器，內容解析器會根據放置機會屬性和中繼資料自訂內容／廣告插入工作流程。

TVSDK包含預設的機會偵測器：

* `PTOpportunityResolver`，瞭解預設廣告提示

TVSDK也包含預設內容解析程式，可根據播放器項目中的中繼資料索引鍵，提供要插入的內容：

* `PTContentResolver`

您可以覆寫預設的機會偵測器和內容解析器，以下列方式自訂廣告工作流程：

* 新增自訂標籤偵測的支援
* 識別廣告插入的自訂標籤
* 建立自訂廣告提供者
* Black out content

<!--<a id="section_C2BA8F50230E4010ABFCD5D976BC1217"></a>-->

TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。

A *`opportunity`* 代表時間軸上的興趣點，通常表示廣告位置機會。 此機會還可以指示可能影響時間線的自定義操作，如封鎖期。 An *`opportunity generator`* designs specific opportunity(tags) in the timeline and notifications TVSDK thathe portunitys have ben tagd. 在時間軸中通過包括非標 `PTTimedMetadata` 準（非HLS）標籤來識別機會。

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會變更時間軸，例如插入一系列廣告、切換至替代串流（封鎖期）或以其他方式編輯時間軸內容。 依預設，TVSDK會呼叫適當的 *`content resolver`* 呼叫，以實作所需的時間軸變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使用來 `PTSDKConfig.setAdTags` 新增更多廣告標籤標籤／提示，讓TVSDK能夠識別並使用並通知您的應用程式， `PTSDKConfig.setSubscribedTags` 其他標籤可能包含廣告工作流程資訊。

自定義解析器的一個可能用途是用於封鎖期。 要處理這些期間，您的應用程式可以實施並註冊一個負責處理封鎖期標籤的封鎖期機會檢測器。 當TVSDK遇到此標籤時，會輪詢所有已註冊的內容解析器，以尋找第一個處理指定標籤的解析器。 在此範例中，它是封鎖內容解析程式，例如，可在標籤所指定的期間內，以播放器上的替代內容取代目前項目。