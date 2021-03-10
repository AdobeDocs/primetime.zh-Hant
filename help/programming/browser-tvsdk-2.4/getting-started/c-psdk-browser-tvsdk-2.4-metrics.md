---
description: 瀏覽器TVSDK提供用於分析和除錯的量度。 您可以使用QoSProvider來取得這些量度。
title: 量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# 量度{#metrics}

瀏覽器TVSDK提供用於分析和除錯的量度。 您可以使用QoSProvider來取得這些量度。

例如：

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

