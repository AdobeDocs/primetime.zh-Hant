---
description: 在Adobe Primetime ad decisioning中，您可以在索引鍵值配對上鎖定廣告。
title: 目標定位資訊
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 目標定位資訊{#targeting-information}

在Adobe Primetime ad decisioning中，您可以在索引鍵值配對上鎖定廣告。

若要將這些索引鍵值配對傳遞至瀏覽器TVSDK：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
