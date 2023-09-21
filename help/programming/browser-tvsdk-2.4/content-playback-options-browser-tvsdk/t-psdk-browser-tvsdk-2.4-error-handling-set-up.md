---
description: 您可以在應用程式中設定一個位置，以回應ERROR狀態來執行錯誤處理。
title: 設定錯誤處理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

您可以在應用程式中設定一個位置，以回應ERROR狀態來執行錯誤處理。

1. 新增事件接聽程式 `AdobePSDK.MediaPlayerStatusChangeEvent`.

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件監聽器中，當 `event.status` 是 `AdobePSDK.MediaPlayerStatus.ERROR`，提供邏輯以處理所有錯誤。
1. 處理錯誤後，重設 `MediaPlayer` 物件或載入新媒體資源。

       當MediaPlayer物件處於ERROR狀態時，除非您完成下列其中一項工作，否則無法結束此狀態：
   
   * 使用重設MediaPlayer物件 `MediaPlayer.reset` 方法。
   * 使用載入新的媒體資源 `MediaPlayer.replaceCurrentResource` 方法。

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
