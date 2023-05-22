---
description: iOS的TVSDK包含多種功能。
title: 黃金時段TVSDK功能
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 黃金時段TVSDK功能 {#primetime-tvsdk-features}

iOS的TVSDK包含多種功能，並提供以下主要功能：

* 視頻點播和即時/線性回放

   * 播放窗口的管理，包括播放、停止、暫停、查找和檢索播放頭位置的方法
   * 支援全事件重播
   * 隱藏字幕(608、WebVTT)和用於增加可訪問性的替代形式音頻
   * DVR功能
   * 自適應比特率(ABR)邏輯和ABR控制的初始設定
   * 訂閱非HLS和HLS標籤
   * 即時清單故障轉移支援

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

* 視頻和廣告跟蹤

   * QoS事件跟蹤
   * 幫助TVSDK和您的應用程式非同步通信視頻、廣告和其他元素的狀態以及日誌活動的通知
   * 與Adobe Analytics和心跳支援整合

* 記錄

   * 調試日誌記錄
