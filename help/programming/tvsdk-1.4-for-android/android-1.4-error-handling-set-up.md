---
description: 設定一個位置來處理錯誤。
title: 設定錯誤處理
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

設定一個位置來處理錯誤。

1. 為實現事件回調函式 `MediaPlayerEvent.STATUS_CHANGED`。

   TVSDK傳遞事件資訊，如 `MediaPlayerStatusChangeEvent` 的雙曲餘切值。
1. 在回調中，返回的狀態為 `MediaPlayerState.ERROR`，提供處理所有錯誤的邏輯。
1. 處理錯誤後，重置 `MediaPlayer` 對象或載入新媒體資源。

   當 `MediaPlayer` 對象處於錯誤狀態，在您使用 `MediaPlayer.reset` 的雙曲餘切值。

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
