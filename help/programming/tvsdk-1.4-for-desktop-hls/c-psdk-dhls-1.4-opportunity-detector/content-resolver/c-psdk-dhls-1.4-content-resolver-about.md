---
description: TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。
seo-description: TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。
seo-title: 機會產生器和內容解決器
title: 機會產生器和內容解決器
uuid: 9eaeeacf-9e7c-4ebb-a91e-fbc53e96d2c3
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 機會產生器和內容解決器{#opportunity-generators-and-content-resolvers}

TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。

A *`opportunity`* 代表時間軸上的興趣點，通常表示廣告位置機會。 此機會還可以指示可能影響時間線的自定義操作，如封鎖期。 An *`opportunity generator`* designs specific opportunity(tags) in the timeline and notifications TVSDK thathe portunitys have ben tagd. 在中的時間軸中可發現機會 `TimedMetadata`。 The `SpliceOutOpportunityGenerator` creates comportiences beased on the objects that are created for each ad tag that heaven been detected in the manifest, and the `TimedMetadata``AdSignalingModeOpportunityGenerator``MediaPlayerItem` created the initial opportient, of the type and its associated ad signaling mode.

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會變更時間軸，例如插入一系列廣告、切換至替代串流（封鎖期）或以其他方式編輯時間軸內容。 依預設，TVSDK會呼叫適當的 *`content resolver`* 呼叫，以實作所需的時間軸變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使用 `PSDKConfig.adTags` 新增更多預設類別的廣告標籤標籤／提示， `SpliceOutOpportunityGenerator` 並使用 `PSDKConfig.setSubscribedTags` ，讓TVSDK可通知您的應用程式其他可能包含廣告工作流程資訊的標籤。

自定義解析器的一個可能用途是用於封鎖期。 要處理這些期間，您的應用程式可以實施並註冊一個負責處理封鎖期標籤的封鎖期機會檢測器。 當TVSDK遇到此標籤時，會輪詢所有已註冊的內容解析器，以尋找第一個處理指定標籤的解析器。 在此範例中，它是封鎖內容解析程式，例如，可在標籤所指定的期間內，以播放器上的替代內容取代目前項目。
