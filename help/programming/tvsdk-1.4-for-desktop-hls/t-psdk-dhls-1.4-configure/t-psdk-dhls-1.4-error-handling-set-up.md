---
description: 設定單一位置以處理錯誤。
seo-description: 設定單一位置以處理錯誤。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 設定錯誤處理{#set-up-error-handling}

設定單一位置以處理錯誤。

1. 實作的事件回呼函式 `MediaPlayerStatusChangeEvent.STATUS_CHANGED`。

   TVSDK會傳遞事件資訊，例如物 `MediaPlayerStatusChangeEvent` 件。
1. 在回呼中，當事件參數的狀態為時， `MediaPlayerStatus.ERROR`提供處理所有錯誤的邏輯。
1. 處理錯誤後，請重設物 `MediaPlayer` 件或載入新媒體資源。

   當對 `MediaPlayer` 像處於ERROR狀態時，除非您重設對象（通過方法）或載入新媒體資源( `MediaPlayer``MediaPlayer.reset``MediaPlayer.replaceCurrentItem`)，否則它無法退出此狀態。

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

