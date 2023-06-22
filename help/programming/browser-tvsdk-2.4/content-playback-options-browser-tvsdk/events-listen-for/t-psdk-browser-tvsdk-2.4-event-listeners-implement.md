---
description: 事件處理常式可讓瀏覽器TVSDK回應事件。
title: 實作事件接聽程式和回呼
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 實作事件接聽程式和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓瀏覽器TVSDK回應事件。

當事件發生時，瀏覽器TVSDK的事件機制會呼叫您註冊的事件處理常式，並將事件資訊傳遞至處理常式。

您的應用程式必須為影響您應用程式的瀏覽器TVSDK事件實作事件接聽程式。

1. 判斷應用程式必須監聽的事件。

   * **必要事件**：接聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `STATUS_CHANGED` 提供播放器狀態，包括錯誤。 任何狀態都可能影響您的播放器的下一步。

   * **其他事件**：選擇性，視您的應用程式而定。

      例如，如果您在播放中加入廣告，請聆聽所有內容 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 實作每個事件的事件接聽程式。

   瀏覽器TVSDK會傳回事件接聽程式回呼的引數值。 這些值會提供有關事件的相關資訊，您可在接聽程式中用來執行適當的動作。

   例如：

   * 事件型別： `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件屬性： `MediaPlayerStatus.<event>` 使用方式如下：

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. 向註冊回呼接聽程式 `MediaPlayer` 物件，使用 `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
