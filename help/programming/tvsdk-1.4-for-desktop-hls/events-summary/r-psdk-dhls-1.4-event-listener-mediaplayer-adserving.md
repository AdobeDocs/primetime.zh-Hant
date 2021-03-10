---
description: TVSDK會根據計時中繼資料作業來調度廣告服務事件。
title: 廣告服務／計時中繼資料事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 0%

---


# 廣告服務／計時中繼資料事件{#ad-serving-timed-metadata-events}

TVSDK會根據計時中繼資料作業來調度廣告服務事件。

要獲得所有此類相關事件的通知，請向`MediaPlayer`對象註冊事件偵聽器，以處理以下事件。

| 事件 | 意義 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已處理ID3計時中繼資料。 |
| TimedMetadataEvent。[TIMED_METADATA_KLIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已處理計時中繼資料，但未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 計時中繼資料可用，且未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已處理計時中繼資料，且未在背景資訊清單中偵測到任何機會。 |