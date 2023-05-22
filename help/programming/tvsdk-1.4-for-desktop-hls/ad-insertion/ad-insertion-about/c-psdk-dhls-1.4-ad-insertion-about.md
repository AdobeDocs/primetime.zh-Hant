---
description: 廣告插入解決了用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。
title: 插入廣告
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 概述 {#inserting-ads-overview}

廣告插入解決了用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。

安 *`ad break`* 包含一個或多個按順序播放的廣告。 TVSDK將廣告作為一個或多個廣告分段的成員插入主內容中。

## 禁用預卷廣告 {#disable-preroll-ads}

要禁用預滾，請更改預設機會生成器以不進行預滾呼叫。 預設機會生成器為：

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
result.push(new AdSignalingModeOpportunityGenerator()); 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```

要禁用即時流上的預滾動，請更改上面的內容，以僅包括SpliceOutOpportunityGenerator:

```
@inheritDoc 
*/ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
if (preroll_enabled == true) { result.push(new AdSignalingModeOpportunityGenerator()); } 
 
result.push(new SpliceOutOpportunityGenerator()); 
return result; 
}
```
