---
description: 'Desktop HLS的TVSDK包含多種功能，並提供下列主要功能 '
title: Primetime TVSDK功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Primetime TVSDK功能{#primetime-tvsdk-features}

Desktop HLS的TVSDK包含多種功能，並提供下列主要功能：

* VOD和即時／線性播放

   * 播放視窗的管理，包括播放、停止、暫停、搜尋及擷取播放磁頭位置的方法。
   * 隱藏字幕(608、708、WebVTT)和替代形式的音訊，以提高協助功能
   * 控制標題中的文字樣式
   * DVR功能，快速前向／快速倒轉（特技播放模式）
   * 即時和VOD內容的特技播放
   * 自適應位速率(ABR)邏輯和ABR控制的初始設定
   * 即時資訊清單容錯支援
   * 可調整的播放緩衝器
   * 302重新導向最佳化
   * 片段持續時間、大小和下載時間追蹤支援

* 廣告

   * VPAID 2.0
   * 用戶端廣告拼接

      * 順暢的廣告插入，包括對VAST/VMAP的支援
      * 支援廣告的自訂提示標籤
      * 支援標籤、取代和刪除C3廣告
      * 包含封鎖信號的可自訂內容／廣告插入工作流程

* 內容保護

   * 存取數位版權管理(DRM)相關服務
   * 播放未加密的HLS串流或使用受保護的HTTP即時串流(PHLS)
   * 基於DRM策略的基於解析度的輸出控制
   * 作業Cookie和媒體驗證Cookie支援
   * 多網域Token封裝

* 視訊和廣告追蹤

   * QoS事件追蹤
   * 協助TVSDK和您的應用程式以非同步方式通訊視訊、廣告和其他元素的狀態，以及該記錄活動的通知。
   * 與Adobe Analytics和心率支援整合

* 記錄

   * 除錯記錄。
   * 片段持續時間、大小和下載時間的追蹤支援。