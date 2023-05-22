---
description: 設定一個位置來處理錯誤。
title: 設定錯誤處理
exl-id: ce4a2954-0166-43af-afdf-0aa24659f1ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

設定一個位置來處理錯誤。

1. 為實現事件回調函式 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`。

   TVSDK傳遞事件資訊，如 `MediaPlayerStatusChangeEvent` 的雙曲餘切值。
1. 在回調中，當事件參數的狀態為 `MediaPlayerStatus.ERROR`，提供處理所有錯誤的邏輯。
1. 處理錯誤後，重置 `MediaPlayer` 對象或載入新媒體資源。

   當 `MediaPlayer` 對象處於ERROR狀態，在您重置 `MediaPlayer` 對象(通過 `MediaPlayer.reset` 方法)或載入新媒體資源( `MediaPlayer.replaceCurrentItem`)。

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
