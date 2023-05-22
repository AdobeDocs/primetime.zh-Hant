---
description: 所有視頻播放器都必須提供清單伺服器用於插入廣告和啟用廣告跟蹤的功能。
title: 視頻播放器要求
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 視頻播放器要求 {#video-player-requirements}

所有視頻播放器都必須提供清單伺服器用於插入廣告和啟用廣告跟蹤的功能。

要使用黃金時段廣告插入API，視頻播放器必須滿足以下條件：

* 可以跟蹤播放內容時的播放頭位置。
* 可以在指定的時間請求跟蹤URL。
* 在支援HLS v3或更高版本的設備平台上運行，包括：

   * PTS不連續點 `EXT-X-DISCONTINUITY` 標籤
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* 在支援HTTP重定向和分析JSON的平台上運行。
* 在支援CORS的平台上運行。