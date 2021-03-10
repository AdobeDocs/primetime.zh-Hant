---
description: 當您的播放包含廣告時，瀏覽器TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。
title: 廣告活動順序
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 廣告活動順序{#order-of-advertising-events}

當您的播放包含廣告時，瀏覽器TVSDK會依一般預期的序列來傳送事件／通知。 您的播放器可以根據預期序列中的事件實施動作。

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

播放廣告時，事件的順序為：

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* 廣告插播中的每個廣告都會傳送下列訊息：

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` （在廣告播放期間多次）
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

下列範例顯示廣告播放事件的典型進展：

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

