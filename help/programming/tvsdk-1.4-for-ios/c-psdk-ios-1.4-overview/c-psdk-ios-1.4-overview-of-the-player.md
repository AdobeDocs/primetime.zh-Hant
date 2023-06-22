---
description: 適用於iOS的TVSDK包含多種功能。
title: Primetime TVSDK功能
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Primetime TVSDK功能 {#primetime-tvsdk-features}

適用於iOS的TVSDK包含多種功能，並提供下列主要功能：

* VOD和即時/線性播放

   * 管理播放視窗，包括播放、停止、暫停、搜尋和擷取播放點位置的方法
   * 支援完整事件重播
   * 隱藏式字幕(608、WebVTT)和替代的音訊形式，可提升協助工具
   * DVR功能
   * 最適化位元速率(ABR)邏輯和ABR控制項的初始設定
   * 訂閱非HLS和HLS標籤
   * 即時資訊清單容錯移轉支援

* 廣告

   * VPAID 2.0
   * 使用者端廣告拼接

      * 順暢的廣告插入，包括支援VAST/VMAP
      * 支援廣告的自訂提示標籤
      * 支援標籤、取代和刪除C3廣告
      * 包含中斷訊號的可自訂內容/廣告插入工作流程

* 內容保護

   * 存取數位版權管理(DRM)相關服務
   * 未加密或使用受保護的HTTP即時資料流(PHLS)播放HLS資料流
   * 以解析度為基礎的輸出控制，以DRM原則為基礎

* 影片和廣告追蹤

   * QoS事件追蹤
   * 可協助TVSDK和您的應用程式以非同步方式溝通影片、廣告和其他元素的狀態，以及該記錄活動的通知
   * 整合Adobe Analytics並支援心率

* 記錄

   * 偵錯記錄
