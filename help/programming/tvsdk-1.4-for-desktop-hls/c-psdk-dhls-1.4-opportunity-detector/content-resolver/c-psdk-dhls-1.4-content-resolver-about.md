---
description: TVSDK提供預設的機會生成器和內容解析器，這些生成器和解析器基於清單中的非標準標籤。 您的應用程式可能需要根據清單中確定的機會（如封鎖期的指示符）更改時間線。
title: 機會生成器和內容解決器
exl-id: 6daf7ff4-10c4-4750-8592-94a2be489473
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# 機會生成器和內容解決器{#opportunity-generators-and-content-resolvers}

TVSDK提供預設的機會生成器和內容解析器，這些生成器和解析器基於清單中的非標準標籤。 您的應用程式可能需要根據清單中確定的機會（如封鎖期的指示符）更改時間線。

安 *`opportunity`* 表示時間線上通常表示廣告投放機會的關注點。 此機會還可以指示可能影響時間線的自定義操作，如封鎖期。 安 *`opportunity generator`* 確定時間線中的特定機會（標籤），並通知TVSDK這些機會已標籤。 在時間表中確定機會 `TimedMetadata`。 的 `SpliceOutOpportunityGenerator` 根據 `TimedMetadata` 為清單中檢測到的每個ad標籤建立的對象，以及 `AdSignalingModeOpportunityGenerator` 建立基於 `MediaPlayerItem` 類型及其關聯的ad信令模式。

當您的應用程式收到有關機會（標籤）的通知時，您的應用程式可能會通過以下方式來改變時間線：插入一系列廣告、切換到備用流（封鎖期）或編輯時間線內容。 預設情況下，TVSDK調用 *`content resolver`* 以實施所需的時間線更改或操作。 您的應用程式可以使用預設的TVSDK播發內容解析程式或註冊其自己的內容解析程式。

您還可以使用 `PSDKConfig.adTags` 為預設添加更多廣告標籤標籤/提示 `SpliceOutOpportunityGenerator` 類和使用 `PSDKConfig.setSubscribedTags` 以便TVSDK可以通知您的應用程式可能包含廣告工作流資訊的其他標籤。

自定義解析器的一個可能用途是用於封鎖期。 要處理這些期間，您的應用程式可以實施並註冊一個負責處理封鎖標籤的封鎖機會檢測器。 當TVSDK遇到此標籤時，它輪詢所有已註冊的內容解析器以查找處理指定標籤的第一個。 在本示例中，它是封鎖內容解析器，例如，它可以在由標籤指定的持續時間內，將當前項目替換為播放器上的備用內容。
