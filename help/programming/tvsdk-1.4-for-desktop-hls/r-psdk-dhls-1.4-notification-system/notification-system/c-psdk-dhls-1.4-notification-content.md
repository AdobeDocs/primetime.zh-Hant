---
description: MediaPlayerNotification提供與播放器狀態相關的資訊。
seo-description: MediaPlayerNotification提供與播放器狀態相關的資訊。
seo-title: 通知內容
title: 通知內容
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 通知內容{#notification-content}

MediaPlayerNotification提供與播放器狀態相關的資訊。

TVSDK提供`MediaPlayerNotification`通知的時間清單。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * 鍵入INFO、WARN或ERROR
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，例如SEEK_ERROR
   * `metadata`:包含通知相關資訊的金鑰／值配對。例如，名為`URL`的索引鍵提供與通知相關的URL值。

   * `innerNotification`:直接影響此通 `MediaPlayerNotification` 知的對其它對象的引用。

您可以將這些資訊儲存在本機以供日後分析，或將它傳送至遠端伺服器以進行記錄和圖形表示。
