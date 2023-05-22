---
description: TVSDK響應定時元資料操作而調度廣告服務事件。
title: 廣告服務/定時元資料事件
exl-id: 875afa2a-a5cc-4192-91e2-5ba7b61abd57
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---

# 廣告服務/定時元資料事件{#ad-serving-timed-metadata-events}

TVSDK響應定時元資料操作而調度廣告服務事件。

要獲知所有此類相關事件，請向 `MediaPlayer` 對象。

| 事件 | 意義 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已處理ID3定時元資料。 |
| TimedMetadataEvent。[TIMED_METADATA_SKPITED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 處理了定時元資料，未檢測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 計時元資料可用，未檢測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 處理了定時元資料，在後台清單中未檢測到任何機會。 |
