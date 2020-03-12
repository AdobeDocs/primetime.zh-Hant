---
description: 設定單一位置以處理錯誤。
seo-description: 設定單一位置以處理錯誤。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 設定錯誤處理{#set-up-error-handling}

設定單一位置以處理錯誤。

1. 實作的事件回呼函式 `MediaPlayerEvent.STATUS_CHANGED`。

   TVSDK會傳遞事件資訊，例如物 `MediaPlayerStatusChangeEvent` 件。
1. 在回呼中，當傳回狀態為時， `MediaPlayerState.ERROR`提供處理所有錯誤的邏輯。
1. 處理錯誤後，請重設物 `MediaPlayer` 件或載入新媒體資源。

   當物 `MediaPlayer` 件處於錯誤狀態時，它會維持在該狀態，直到您使用方法重設它 `MediaPlayer.reset` 為止。

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

