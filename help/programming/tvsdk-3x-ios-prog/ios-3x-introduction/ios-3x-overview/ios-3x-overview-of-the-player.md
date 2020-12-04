---
description: 適用於Android 3.4的TVSDK包含多種可在播放器中實作的功能。
seo-description: 適用於Android 3.4的TVSDK包含多種可在播放器中實作的功能。
seo-title: Primetime TVSDK功能
title: Primetime TVSDK功能
uuid: 6e26c09c-2858-47d1-80e8-1d7c6a468b86
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Primetime TVSDK功能{#primetime-tvsdk-features}

適用於iOS的TVSDK包含多種可在播放器中實作的功能。

TVSDK功能：

* **VOD和即時／線性播放**

   * 播放視窗的管理，包括播放、停止、暫停、搜尋及擷取播放磁頭位置的方法
   * 支援全事件重播
   * 隱藏字幕(608、708、WebVTT)和替代形式的音訊，以提高協助功能
   * 標題中的文字樣式控制
   * DVR功能、快進和快倒帶（後兩者稱為&#x200B;*trick-play mode*）
   * 自適應位速率(ABR)邏輯和ABR控制的初始設定
   * 即時資訊清單容錯支援
   * 可調整的播放緩衝器
   * 片段持續時間、大小和下載時間追蹤支援

* **廣告**

   * VPAID 2.0
   * 用戶端廣告拼接

      * 順暢的廣告插入，包括對VAST/VMAP的支援
      * 支援廣告的自訂提示標籤
      * 支援標籤、取代和刪除C3廣告
      * 包含封鎖信號的可自訂內容／廣告插入工作流程

* **內容保護**

   * 存取數位版權管理(DRM)相關服務
   * 播放未加密的HLS串流或使用受保護的HTTP即時串流(PHLS)
   * 基於DRM策略的基於解析度的輸出控制

* **視訊和廣告追蹤**

   * QoS事件追蹤
   * 協助TVSDK和您的應用程式以非同步方式通訊視訊、廣告和其他元素狀態的通知。 通知也記錄活動。

* **記錄**

   * 除錯記錄
   * 片段持續時間、大小和下載時間的追蹤支援。