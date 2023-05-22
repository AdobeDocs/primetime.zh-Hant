---
description: 當播放包括廣告時，瀏覽器TVSDK會按通常預期的序列發送事件/通知。 您的玩家可以根據預期序列中的事件執行操作。
title: 廣告活動順序
exl-id: fcc40aa8-9364-40a8-b2f2-9327e24819af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 廣告活動順序{#order-of-advertising-events}

當播放包括廣告時，瀏覽器TVSDK會按通常預期的序列發送事件/通知。 您的玩家可以根據預期序列中的事件執行操作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

在播放廣告時，事件的順序是：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 廣告分段中的每個廣告都派發以下內容：

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` （廣告播放期間多次）
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

以下示例顯示廣告播放事件的典型進展：

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
