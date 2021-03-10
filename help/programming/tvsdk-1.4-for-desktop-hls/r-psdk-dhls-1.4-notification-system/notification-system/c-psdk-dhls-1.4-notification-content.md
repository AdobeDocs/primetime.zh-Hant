---
description: MediaPlayerNotification提供與播放器狀態相關的資訊。
title: 通知內容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
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
