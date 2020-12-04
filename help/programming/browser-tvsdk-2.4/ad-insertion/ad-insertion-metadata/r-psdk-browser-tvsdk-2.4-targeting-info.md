---
description: 在Adobe Primetime廣告決策中，您可以針對關鍵值配對來定位廣告。
seo-description: 在Adobe Primetime廣告決策中，您可以針對關鍵值配對來定位廣告。
seo-title: 定位資訊
title: 定位資訊
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# 定位資訊{#targeting-information}

在Adobe Primetime廣告決策中，您可以針對關鍵值配對來定位廣告。

若要將這些鍵值配對傳遞至瀏覽器TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

