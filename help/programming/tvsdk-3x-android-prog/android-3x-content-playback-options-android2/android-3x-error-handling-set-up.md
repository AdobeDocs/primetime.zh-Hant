---
description: 您可以設定一個空格來處理錯誤。
title: 設定錯誤處理
exl-id: 9b83b47e-6d30-452b-87c3-1e3a139f2e69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# 設定錯誤處理 {#set-up-error-handling}

您可以設定一個空格來處理錯誤。

1. 實作事件回呼函式 `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK會傳遞事件資訊，例如 `MediaPlayerStatusChangeEvent` 物件。
1. 在回呼中，當傳回的狀態為 `MediaPlayerStatus.ERROR`，提供邏輯以處理所有錯誤。
1. 處理錯誤後，重設 `MediaPlayer` 物件或載入新媒體資源。

   當 `MediaPlayer` 物件處於錯誤狀態，除非您使用 `MediaPlayer.reset` 方法。

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
