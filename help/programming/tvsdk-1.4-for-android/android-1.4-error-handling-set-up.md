---
description: 設定處理錯誤的單一位置。
title: 設定錯誤處理
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

設定處理錯誤的單一位置。

1. 實作事件回呼函式 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK會傳遞事件資訊，例如 `MediaPlayerStatusChangeEvent` 物件。
1. 在回呼中，當傳回的狀態為 `MediaPlayerState.ERROR`，提供邏輯以處理所有錯誤。
1. 處理錯誤後，重設 `MediaPlayer` 物件或載入新媒體資源。

   當 `MediaPlayer` 物件處於錯誤狀態，除非您使用 `MediaPlayer.reset` 方法。

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

例如：

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```
