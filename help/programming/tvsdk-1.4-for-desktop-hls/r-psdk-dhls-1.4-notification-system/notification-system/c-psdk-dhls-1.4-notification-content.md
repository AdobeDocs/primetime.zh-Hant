---
description: MediaPlayerNotification提供與播放器狀態相關的資訊。
title: 通知內容
exl-id: dc46f717-f08b-4d52-82ea-88107076f4fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 通知內容{#notification-content}

MediaPlayerNotification提供與播放器狀態相關的資訊。

TVSDK提供以下專案的時間順序清單： `MediaPlayerNotification` 通知。 每個通知都包含下列資訊：

* 時間戳記
* 包含下列元素的診斷中繼資料：

   * 輸入INFO、WARN或ERROR
   * `code`：通知的數字表示法。
   * `name`：可讀取的通知說明，例如SEEK_ERROR
   * `metadata`：包含通知相關資訊的索引鍵/值組。 例如，名為的金鑰 `URL` 提供一個值，該值為與通知相關的URL。

   * `innerNotification`：對另一個的參照 `MediaPlayerNotification` 直接影響此通知的物件。

您可以將此資訊儲存在本機，供日後分析使用，或傳送至遠端伺服器以供記錄及圖形化顯示。
