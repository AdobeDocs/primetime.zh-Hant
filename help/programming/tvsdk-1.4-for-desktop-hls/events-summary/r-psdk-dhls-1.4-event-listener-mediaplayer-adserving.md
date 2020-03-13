---
description: TVSDK會根據計時中繼資料作業來調度廣告服務事件。
seo-description: TVSDK會根據計時中繼資料作業來調度廣告服務事件。
seo-title: 廣告服務／計時中繼資料事件
title: 廣告服務／計時中繼資料事件
uuid: fd50a937-0c9b-4c47-acb2-1ffc0592ad54
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 廣告服務／計時中繼資料事件{#ad-serving-timed-metadata-events}

TVSDK會根據計時中繼資料作業來調度廣告服務事件。

要獲得所有此類相關事件的通知，請向以下事件的對 `MediaPlayer` 像註冊事件偵聽器。

| 事件 | 意義 |
|---|---|
| TimedMetadataEvent。[TIMED_METADATA_ID3_ADDED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_ID3_ADDED) | 已處理ID3計時中繼資料。 |
| TimedMetadataEvent。[TIMED_METADATA_KRIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_SKIPPED) | 已處理計時中繼資料，但未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_AVAILABLE) | 計時中繼資料可用，且未偵測到任何機會。 |
| TimedMetadataEvent。[TIMED_METADATA_IN_BACKGROUND](https://help.stage.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_2.3/com/adobe/tvsdk/mediacore/events/TimedMetadataEvent.html#TIMED_METADATA_IN_BACKGROUND) | 已處理計時中繼資料，且未在背景資訊清單中偵測到任何機會。 |