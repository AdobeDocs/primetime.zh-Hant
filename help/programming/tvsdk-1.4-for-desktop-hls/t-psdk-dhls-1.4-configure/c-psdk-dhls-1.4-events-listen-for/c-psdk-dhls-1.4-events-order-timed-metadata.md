---
description: TVSDK會在遇到預設或自訂標籤或資訊清單中的播放清單變更時，傳送定時中繼資料事件，並產生定時中繼資料。 事件會依照其顯示在資訊清單中的順序傳送。
title: 定時中繼資料事件
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定時中繼資料事件{#timed-metadata-events}

TVSDK會在遇到預設或自訂標籤或資訊清單中的播放清單變更時，傳送定時中繼資料事件，並產生定時中繼資料。 事件會依照其顯示在資訊清單中的順序傳送。

您的播放器會根據下列事件實作動作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`：在處理ID3計時中繼資料時傳送。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`：在處理計時中繼資料且未偵測到任何機會時傳送。
