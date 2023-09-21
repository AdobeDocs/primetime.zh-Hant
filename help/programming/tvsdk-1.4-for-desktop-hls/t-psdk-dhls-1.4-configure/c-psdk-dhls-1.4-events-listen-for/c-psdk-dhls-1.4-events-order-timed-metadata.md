---
description: TVSDK會在發生預設或自訂標籤或資訊清單中的播放清單變更時，傳送定時中繼資料事件並產生定時中繼資料。 事件會依照其出現在資訊清單中的順序傳送。
title: 定時中繼資料事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定時中繼資料事件{#timed-metadata-events}

TVSDK會在發生預設或自訂標籤或資訊清單中的播放清單變更時，傳送定時中繼資料事件並產生定時中繼資料。 事件會依照其出現在資訊清單中的順序傳送。

您的播放器會根據下列事件實作動作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`：在處理ID3計時中繼資料時傳送。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`：在處理定時中繼資料且未偵測到任何商機時傳送。
