---
description: TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。
title: 機會產生器和內容解決器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# 機會生成器和內容解析器{#opportunity-generators-and-content-resolvers}

TVSDK提供預設的機會產生器和內容解析器，可將廣告置於時間軸中，而這些產生器和解析器是以資訊清單中的非標準標籤為基礎。 您的應用程式可能需要根據資訊清單中識別的商機（例如封鎖期的指標）來變更時間軸。

*`opportunity`*&#x200B;代表時間軸上的興趣點，通常表示廣告投放機會。 此機會還可以指示可能影響時間線的自定義操作，如封鎖期。 *`opportunity generator`*&#x200B;會在時間軸中識別特定商機（標籤），並通知TVSDK這些商機已標籤。 在`TimedMetadata`的時間軸中識別機會。 `SpliceOutOpportunityGenerator`根據為清單中檢測到的每個廣告標籤建立的`TimedMetadata`對象建立機會，而`AdSignalingModeOpportunityGenerator`建立基於`MediaPlayerItem`類型及其相關廣告信令模式的初始機會。

當您的應用程式收到機會（標籤）的通知時，您的應用程式可能會變更時間軸，例如插入一系列廣告、切換至替代串流（封鎖期）或以其他方式編輯時間軸內容。 依預設，TVSDK會呼叫適當的&#x200B;*`content resolver`*，以實作所需的時間軸變更或動作。 您的應用程式可以使用預設的TVSDK廣告內容解析程式，或註冊其專屬的內容解析程式。

您也可以使用`PSDKConfig.adTags`新增更多預設`SpliceOutOpportunityGenerator`類別的廣告標籤標籤／提示，並使用`PSDKConfig.setSubscribedTags`，讓TVSDK通知您的應用程式其他可能包含廣告工作流程資訊的標籤。

自定義解析器的一個可能用途是用於封鎖期。 要處理這些期間，您的應用程式可以實施並註冊一個負責處理封鎖期標籤的封鎖期機會檢測器。 當TVSDK遇到此標籤時，會輪詢所有已註冊的內容解析器，以尋找第一個處理指定標籤的解析器。 在此範例中，它是封鎖內容解析程式，例如，可在標籤所指定的期間內，以播放器上的替代內容取代目前項目。
