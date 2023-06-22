---
description: 您可以在應用程式中設定一個位置，以執行錯誤處理以回應ERROR狀態。
title: 設定錯誤處理
exl-id: c0ce1d80-85d5-4344-9ab0-bd56906421cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

您可以在應用程式中設定一個位置，以執行錯誤處理以回應ERROR狀態。

1. 新增事件接聽程式 `AdobePSDK.MediaPlayerStatusChangeEvent`.

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在您的事件監聽器中，當 `event.status` 是 `AdobePSDK.MediaPlayerStatus.ERROR`，提供處理所有錯誤的邏輯。
1. 處理錯誤後，重設 `MediaPlayer` 物件或載入新媒體資源。

       當MediaPlayer物件處於ERROR狀態時，您必須完成下列其中一項工作，才能結束此狀態：
   
   * 使用重設MediaPlayer物件 `MediaPlayer.reset` 方法。
   * 使用載入新媒體資源 `MediaPlayer.replaceCurrentResource` 方法。

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

例如：

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```
