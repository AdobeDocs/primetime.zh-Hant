---
description: TVSDK會傳送廣告服務事件以回應計時的中繼資料作業。
title: 廣告服務/計時中繼資料事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 廣告服務/計時中繼資料事件{#ad-serving-timed-metadata-events}

TVSDK會傳送廣告服務事件以回應計時的中繼資料作業。

若要收到有關所有相關事件的通知，請將事件接聽程式註冊到 `MediaPlayer` 物件。

| 事件 | 含義 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已處理ID3計時中繼資料。 |
| TimedMetadataEvent。[TIMED_METADATA_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已處理定時中繼資料，但未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 計時中繼資料可供使用，而且未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已處理定時中繼資料，且在背景資訊清單中未偵測到任何機會。 |
