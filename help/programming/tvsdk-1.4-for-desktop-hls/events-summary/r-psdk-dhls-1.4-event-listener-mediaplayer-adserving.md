---
description: TVSDK會傳送廣告服務事件以回應計時中繼資料作業。
title: 廣告服務/計時中繼資料事件
exl-id: 875afa2a-a5cc-4192-91e2-5ba7b61abd57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 廣告服務/計時中繼資料事件{#ad-serving-timed-metadata-events}

TVSDK會傳送廣告服務事件以回應計時中繼資料作業。

若要收到所有相關事件的通知，請透過以下網址註冊事件監聽器： `MediaPlayer` 物件。

| 事件 | 含義 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已處理ID3計時中繼資料。 |
| TimedMetadataEvent。[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已處理定時中繼資料，但未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 計時中繼資料可供使用，且未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已處理定時中繼資料，且在背景資訊清單中偵測不到任何機會。 |
