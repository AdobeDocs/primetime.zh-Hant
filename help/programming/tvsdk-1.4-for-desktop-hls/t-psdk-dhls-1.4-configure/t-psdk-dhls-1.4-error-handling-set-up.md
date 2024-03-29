---
description: 設定處理錯誤的單一位置。
title: 設定錯誤處理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

設定處理錯誤的單一位置。

1. 實作事件回呼函式 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   TVSDK會傳遞事件資訊，例如 `MediaPlayerStatusChangeEvent` 物件。
1. 在回撥中，當來自事件引數的狀態為 `MediaPlayerStatus.ERROR`，提供邏輯以處理所有錯誤。
1. 處理錯誤後，重設 `MediaPlayer` 物件或載入新媒體資源。

   當 `MediaPlayer` 物件處於ERROR狀態，除非重設 `MediaPlayer` 物件(透過 `MediaPlayer.reset` 方法)或載入新媒體資源( `MediaPlayer.replaceCurrentItem`)。

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

例如：

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```
