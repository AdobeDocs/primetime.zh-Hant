---
description: TVSDK會在遇到預設或自訂標籤時，或在清單中變更播放清單時，調度計時中繼資料事件並產生計時中繼資料。 事件會依照事件在資訊清單中的顯示順序來傳送。
seo-description: TVSDK會在遇到預設或自訂標籤時，或在清單中變更播放清單時，調度計時中繼資料事件並產生計時中繼資料。 事件會依照事件在資訊清單中的顯示順序來傳送。
seo-title: 計時中繼資料事件
title: 計時中繼資料事件
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# 計時中繼資料事件{#timed-metadata-events}

TVSDK會在遇到預設或自訂標籤時，或在清單中變更播放清單時，調度計時中繼資料事件並產生計時中繼資料。 事件會依照事件在資訊清單中的顯示順序來傳送。

您的播放器會根據下列事件實作動作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:在處理ID3計時中繼資料時傳送。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:在處理計時中繼資料且未偵測到任何機會時傳送。

