---
description: 所有視訊播放程式都必須提供資訊清單伺服器所仰賴的功能，以插入廣告並啟用廣告追蹤。
seo-description: 所有視訊播放程式都必須提供資訊清單伺服器所仰賴的功能，以插入廣告並啟用廣告追蹤。
seo-title: 視訊播放器需求
title: 視訊播放器需求
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 視訊播放器需求{#video-player-requirements}

所有視訊播放程式都必須提供資訊清單伺服器所仰賴的功能，以插入廣告並啟用廣告追蹤。

若要使用Primetime廣告插入API，視訊播放器必須符合下列條件：

* 可在播放內容時追蹤播放磁頭位置。
* 可在指定的時間要求追蹤URL。
* 在支援HLS v3或更新版本的裝置平台上執行，包括：

   * 由`EXT-X-DISCONTINUITY`標籤標籤的PTS不連續
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* 在支援HTTP重新導向和剖析JSON的平台上執行。
* 網路播放器必須在支援CORS的平台上執行。