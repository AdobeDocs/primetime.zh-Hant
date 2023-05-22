---
description: 用於Desktop HLS的TVSDK包含多種功能，並提供以下主要功能
title: 黃金時段TVSDK功能
exl-id: d78ca77e-b29c-4fae-8ab9-edc55ab12847
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 黃金時段TVSDK功能{#primetime-tvsdk-features}

用於Desktop HLS的TVSDK包含多種功能，並提供以下主要功能：

* 視頻點播和即時/線性回放

   * 播放窗口的管理，包括播放、停止、暫停、查找和檢索播放頭位置的方法。
   * 隱藏字幕(608、708、WebVTT)和替代形式的音頻，以增加可訪問性
   * 字幕中文本樣式的控制
   * DVR功能，快速前進/快速倒帶（特技播放模式）
   * 即時和視頻點播內容的特技播放
   * 自適應比特率(ABR)邏輯和ABR控制的初始設定
   * 即時清單故障轉移支援
   * 可調回放緩衝器
   * 302重定向優化
   * 片段持續時間、大小和下載時間跟蹤支援

* 廣告

   * VPAID 2.0
   * 客戶端廣告拼接

      * 無縫廣告插入，包括對VAST/VMAP的支援
      * 支援廣告的自定義提示標籤
      * 支援標籤、替換和刪除C3廣告
      * 包括封鎖信號的可定製內容/廣告插入工作流

* 內容保護

   * 訪問數字版權管理(DRM)相關服務
   * HLS流的回放未加密或使用受保護的HTTP即時流(PHLS)
   * 基於DRM策略的基於解析度的輸出控制
   * 會話Cookie和媒體身份驗證Cookie支援
   * 多域令牌打包

* 視頻和廣告跟蹤

   * QoS事件跟蹤
   * 幫助TVSDK和您的應用程式非同步通信有關視頻、廣告和其他元素的狀態以及日誌活動的通知。
   * 與Adobe Analytics和心跳支援整合

* 記錄

   * 調試日誌記錄。
   * 對片段持續時間、大小和下載時間的跟蹤支援。
