---
description: 您可以設定一個邊來處理錯誤。
seo-description: 您可以設定一個邊來處理錯誤。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# 設定錯誤處理{#set-up-error-handling}

您可以設定一個邊來處理錯誤。

1. 實作`MediaPlayerEvent.STATUS_CHANGED`的事件回呼函式。

   TVSDK會傳遞事件資訊，例如`MediaPlayerStatusChangeEvent`物件。
1. 在回呼中，當傳回的狀態為`MediaPlayerStatus.ERROR`時，請提供處理所有錯誤的邏輯。
1. 處理錯誤後，請重設`MediaPlayer`物件或載入新媒體資源。

   當`MediaPlayer`對象處於錯誤狀態時，它將保持該狀態，直到您使用`MediaPlayer.reset`方法重置它為止。

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

例如：

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```

