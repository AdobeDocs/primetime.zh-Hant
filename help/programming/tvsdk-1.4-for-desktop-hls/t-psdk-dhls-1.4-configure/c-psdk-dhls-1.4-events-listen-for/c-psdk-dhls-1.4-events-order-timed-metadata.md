---
description: TVSDK在遇到預設標籤或自定義標籤或播放清單在清單中發生更改時調度定時元資料事件並生成定時元資料。 事件按它們在清單中的顯示順序調度。
title: 定時元資料事件
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定時元資料事件{#timed-metadata-events}

TVSDK在遇到預設標籤或自定義標籤或播放清單在清單中發生更改時調度定時元資料事件並生成定時元資料。 事件按它們在清單中的顯示順序調度。

您的播放器根據以下事件執行操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:處理ID3定時元資料時調度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:在處理定時元資料且未檢測到任何機會時調度。
