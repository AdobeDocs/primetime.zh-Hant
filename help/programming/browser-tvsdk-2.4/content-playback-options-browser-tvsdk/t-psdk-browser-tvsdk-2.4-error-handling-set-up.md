---
description: 您可以在應用程式中設定一個位置，以因應ERROR狀態執行錯誤處理。
seo-description: 您可以在應用程式中設定一個位置，以因應ERROR狀態執行錯誤處理。
seo-title: 設定錯誤處理
title: 設定錯誤處理
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 2%

---


# 設定錯誤處理{#set-up-error-handling}

您可以在應用程式中設定一個位置，以因應ERROR狀態執行錯誤處理。

1. 為`AdobePSDK.MediaPlayerStatusChangeEvent`添加事件偵聽器。

   例如：

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. 在事件偵聽器中，當`event.status`為`AdobePSDK.MediaPlayerStatus.ERROR`時，提供處理所有錯誤的邏輯。
1. 處理錯誤後，請重設`MediaPlayer`物件或載入新媒體資源。

       當MediaPlayer物件處於ERROR狀態時，您必須完成下列其中一項工作，它才能退出此狀態：
   
   * 使用`MediaPlayer.reset`方法重設MediaPlayer物件。
   * 使用`MediaPlayer.replaceCurrentResource`方法載入新媒體資源。

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

