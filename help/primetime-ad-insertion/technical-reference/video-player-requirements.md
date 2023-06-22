---
description: 所有影片播放器都必須提供資訊清單伺服器所依賴的功能，才能插入廣告及啟用廣告追蹤。
title: 視訊播放器需求
exl-id: 23134e4c-6902-4b97-bf15-4524f47850e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 視訊播放器需求 {#video-player-requirements}

所有影片播放器都必須提供資訊清單伺服器所依賴的功能，才能插入廣告及啟用廣告追蹤。

若要使用Primetime廣告插入API，視訊播放器必須滿足以下條件：

* 可在播放內容時追蹤播放點位置。
* 可以在指定的時間要求追蹤URL。
* 在支援HLS v3或更新版本的裝置平台上執行，包括：

   * PTS不連續性，標籤方式為 `EXT-X-DISCONTINUITY` 標籤
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* 在支援HTTP重新導向和剖析JSON的平台上執行。
* 網頁型播放器必須在支援CORS的平台上執行。
