---
description: 廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。
seo-description: 廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。
seo-title: 插入廣告
title: 插入廣告
uuid: 25c79822-a861-427b-b6a8-24714b21aae4
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概觀 {#inserting-ads-overview}

廣告插入可解析隨選視訊(VOD)、即時串流以及具有廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需要求，接收指定內容的廣告資訊，並將廣告分階段置於內容中。

包含 *`ad break`* 依序播放的一或多個廣告。 TVSDK會將廣告插入主要內容中，作為一個或多個廣告插播的成員。

## 停用前段廣告 {#disable-preroll-ads}

要禁用前滾，請更改預設的機會生成器以不進行前滾呼叫。 預設的機會生成器是：

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

要禁用即時流上的前滾，請更改上述內容，使其僅包括SpliceOutOpportunityGenerator:

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
