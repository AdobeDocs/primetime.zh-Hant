---
description: 事件處理程式允許瀏覽器TVSDK響應事件。
title: 實現事件偵聽器和回調
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 實現事件偵聽器和回調{#implement-event-listeners-and-callbacks}

事件處理程式允許瀏覽器TVSDK響應事件。

當發生事件時，瀏覽器TVSDK的事件機制將調用您註冊的事件處理程式並將事件資訊傳遞給處理程式。

您的應用程式必須為影響您的應用程式的瀏覽器TVSDK事件實現事件偵聽器。

1. 確定應用程式必須偵聽哪些事件。

   * **必需事件**:收聽所有播放事件。

      >[!IMPORTANT]
      >
      >播放事件 `STATUS_CHANGED` 提供播放器狀態，包括錯誤。 任何狀態都可能影響玩家的下一步。

   * **其他事件**:可選，具體取決於您的應用程式。

      例如，如果在播放中加入廣告，請傾聽所有 `AdBreakPlaybackEvent` 和 `AdPlaybackEvent` 事件。

1. 為每個事件實現事件偵聽器。

   瀏覽器TVSDK將參數值返回到事件監聽器回調。 這些值提供了有關事件的相關資訊，您可以在監聽器中使用這些事件執行相應的操作。

   例如：

   * 事件類型： `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * 事件屬性： `MediaPlayerStatus.<event>` 如下：

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

1. 將回調偵聽器註冊到 `MediaPlayer` 對象使用 `MediaPlayer.addEventListener`。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
