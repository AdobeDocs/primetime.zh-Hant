---
description: 事件處理常式可讓瀏覽器TVSDK回應事件。
seo-description: 事件處理常式可讓瀏覽器TVSDK回應事件。
seo-title: 實作事件偵聽器和回呼
title: 實作事件偵聽器和回呼
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 實作事件偵聽器和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓瀏覽器TVSDK回應事件。

發生事件時，瀏覽器TVSDK的事件機制會呼叫您已註冊的事件處理常式，並將事件資訊傳遞給處理常式。

您的應用程式必須針對影響您應用程式的瀏覽器TVSDK事件實作事件偵聽器。

1. 決定您的應用程式必須監聽哪些事件。

   * **必要事件**:監聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `STATUS_CHANGED` 提供播放器狀態，包括錯誤。 任何狀態都可能會影響您播放器的下一步。

   * **其他事件**:可選，視您的應用程式而定。

      例如，如果您在播放中加入廣告，請監聽所有 `AdBreakPlaybackEvent` 和事 `AdPlaybackEvent` 件。

1. 為每個事件實施事件偵聽器。

   瀏覽器TVSDK會將參數值傳回至您的事件接聽程式回呼。 這些值會提供有關事件的相關資訊，您可在監聽程式中用來執行適當動作。

   例如：

   * 事件類型： `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件屬性： `MediaPlayerStatus.<event>` 使用如下：

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

1. 使用將回呼偵聽程式註冊 `MediaPlayer` 到對象中 `MediaPlayer.addEventListener`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
