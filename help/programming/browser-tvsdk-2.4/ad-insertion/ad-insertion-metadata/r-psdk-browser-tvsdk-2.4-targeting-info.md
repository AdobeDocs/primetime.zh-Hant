---
description: 在Adobe Primetime ad decisioning中，您可以在索引鍵值配對上鎖定廣告。
title: 目標定位資訊
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 目標定位資訊{#targeting-information}

在Adobe Primetime ad decisioning中，您可以在索引鍵值配對上鎖定廣告。

若要將這些機碼值組傳遞至瀏覽器TVSDK：

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
