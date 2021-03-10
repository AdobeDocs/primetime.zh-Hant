---
description: 事件處理常式可讓瀏覽器TVSDK回應事件。
title: 實作事件偵聽器和回呼
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# 實施事件偵聽器和回呼{#implement-event-listeners-and-callbacks}

事件處理常式可讓瀏覽器TVSDK回應事件。

發生事件時，瀏覽器TVSDK的事件機制會呼叫您已註冊的事件處理常式，並將事件資訊傳遞給處理常式。

您的應用程式必須針對影響您應用程式的瀏覽器TVSDK事件實作事件偵聽器。

1. 決定您的應用程式必須監聽哪些事件。

   * **必要事件**:監聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件`STATUS_CHANGED`提供播放器狀態，包括錯誤。 任何狀態都可能會影響您播放器的下一步。

   * **其他事件**:可選，視您的應用程式而定。

      例如，如果您在播放中加入廣告，請監聽所有`AdBreakPlaybackEvent`和`AdPlaybackEvent`事件。

1. 為每個事件實施事件偵聽器。

   瀏覽器TVSDK會將參數值傳回至您的事件接聽程式回呼。 這些值會提供有關事件的相關資訊，您可在監聽程式中用來執行適當動作。

   例如：

   * 事件類型：`AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件屬性：`MediaPlayerStatus.<event>`的用法如下：

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

1. 使用`MediaPlayer.addEventListener`將回呼偵聽器註冊到`MediaPlayer`對象。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
