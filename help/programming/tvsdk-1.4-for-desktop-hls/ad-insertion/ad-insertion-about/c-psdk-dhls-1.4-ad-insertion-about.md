---
description: 廣告插入解析視訊點播(VOD) 、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。
title: 插入廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 概觀 {#inserting-ads-overview}

廣告插入解析視訊點播(VOD) 、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。

一個 *`ad break`* 包含一或多個循序播放的廣告。 TVSDK會將廣告插入主要內容，作為一或多個廣告插播的成員。

## 停用前段廣告 {#disable-preroll-ads}

若要停用前段通話，請變更預設機會產生器，使其不進行前段通話。 預設機會產生器為：

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

若要在即時資料流上停用前置滾動，請變更上述專案以僅包含SpliceOutOpportunityGenerator：

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
