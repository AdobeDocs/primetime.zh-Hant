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

TVSDK提供按時間順序排列的 `MediaPlayerNotification` 通知。 每個通知都包含以下資訊：

* 時間戳
* 包含以下元素的診斷元資料：

   * 類型資訊、警告或錯誤
   * `code`:通知的數字表示。
   * `name`:通知的可人讀描述，如SEEK_ERROR
   * `metadata`:包含有關通知的相關資訊的鍵/值對。 例如，名為 `URL` 提供與通知相關的URL的值。

   * `innerNotification`:對另一個的引用 `MediaPlayerNotification` 直接影響此通知的對象。

您可以將此資訊本地儲存以供以後分析，或將其發送到遠程伺服器以進行日誌記錄和圖形表示。
