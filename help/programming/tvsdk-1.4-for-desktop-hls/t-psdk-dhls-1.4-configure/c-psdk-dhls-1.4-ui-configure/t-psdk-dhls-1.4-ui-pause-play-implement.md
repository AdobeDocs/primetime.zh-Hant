---
description: 可以添加TVSDK行為以暫停和播放按鈕。
title: 播放並暫停視頻
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 播放並暫停視頻{#play-and-pause-a-video}

可以添加TVSDK行為以暫停和播放按鈕。

1. 建立執行以下操作的暫停/播放按鈕。
   1. 等待玩家至少處於PREPARED狀態。
   1. 要開始播放，請調用TVSDK播放方法：

      ```
      function play():void;
      ```

   1. 要暫停播放，請調用TVSDK暫停方法：

      ```
      function pause():void;
      ```

1. 使用回調 `MediaPlayerStatusChangeEvent.STATUS_CHANGED` 事件，檢查錯誤或執行其他相應操作。

   調用pause或play方法時，TVSDK將調用此回調。 TVSDK傳遞有關回調中狀態更改的資訊，包括新狀態，如PAUSED或PLAYING。
