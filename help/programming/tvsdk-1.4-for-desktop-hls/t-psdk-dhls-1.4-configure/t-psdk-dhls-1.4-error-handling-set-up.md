---
description: 設定單一位置以處理錯誤。
seo-description: 設定單一位置以處理錯誤。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# 設定錯誤處理{#set-up-error-handling}

設定單一位置以處理錯誤。

1. 實作`MediaPlayerStatusChangeEvent.STATUS_CHANGED`的事件回呼函式。

   TVSDK會傳遞事件資訊，例如`MediaPlayerStatusChangeEvent`物件。
1. 在回呼中，當事件參數的狀態為`MediaPlayerStatus.ERROR`時，提供處理所有錯誤的邏輯。
1. 處理錯誤後，請重設`MediaPlayer`物件或載入新媒體資源。

   當`MediaPlayer`對象處於ERROR狀態時，除非您重設`MediaPlayer`對象（通過`MediaPlayer.reset`方法）或載入新媒體資源(`MediaPlayer.replaceCurrentItem`)，否則它無法退出此狀態。

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

