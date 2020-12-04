---
description: 您可以設定一個邊來處理錯誤。
seo-description: 您可以設定一個邊來處理錯誤。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: 7c122830-6259-4e95-882e-fb1700454e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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
