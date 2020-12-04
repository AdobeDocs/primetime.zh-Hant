---
description: 瀏覽器TVSDK提供用於分析和除錯的量度。 您可以使用QoSProvider來取得這些量度。
seo-description: 瀏覽器TVSDK提供用於分析和除錯的量度。 您可以使用QoSProvider來取得這些量度。
seo-title: 量度
title: 量度
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 3%

---


# 量度{#metrics}

瀏覽器TVSDK提供用於分析和除錯的量度。 您可以使用QoSProvider來取得這些量度。

例如：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

