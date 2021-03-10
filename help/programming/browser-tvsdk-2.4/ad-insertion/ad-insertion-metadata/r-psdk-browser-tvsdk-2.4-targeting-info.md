---
description: 在Adobe Primetime廣告決策中，您可以針對關鍵值對來定位廣告。
title: 定位資訊
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 定位資訊{#targeting-information}

在Adobe Primetime廣告決策中，您可以針對關鍵值對來定位廣告。

若要將這些鍵值配對傳遞至瀏覽器TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

