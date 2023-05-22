---
description: 在Adobe Primetime廣告決策中，您可以針對關鍵值對投放廣告。
title: 目標資訊
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 目標資訊{#targeting-information}

在Adobe Primetime廣告決策中，您可以針對關鍵值對投放廣告。

要將這些鍵值對傳遞到瀏覽器TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
