---
description: 您可以在應用程式中設定一個位置以響應ERROR狀態執行錯誤處理。
title: 設定錯誤處理
exl-id: c0ce1d80-85d5-4344-9ab0-bd56906421cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 設定錯誤處理{#set-up-error-handling}

您可以在應用程式中設定一個位置以響應ERROR狀態執行錯誤處理。

1. 為添加事件偵聽器 `AdobePSDK.MediaPlayerStatusChangeEvent`。

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件偵聽器中，當 `event.status` 是 `AdobePSDK.MediaPlayerStatus.ERROR`，提供處理所有錯誤的邏輯。
1. 處理錯誤後，重置 `MediaPlayer` 對象或載入新媒體資源。

       當MediaPlayer對象處於ERROR狀態時，在您完成以下任務之一之前，它無法退出此狀態：
   
   * 使用 `MediaPlayer.reset` 的雙曲餘切值。
   * 使用 `MediaPlayer.replaceCurrentResource` 的雙曲餘切值。

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
