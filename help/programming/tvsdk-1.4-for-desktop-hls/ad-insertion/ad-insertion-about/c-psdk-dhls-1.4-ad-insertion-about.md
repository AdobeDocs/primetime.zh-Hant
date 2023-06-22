---
description: 廣告插入會解析視訊點播(VOD) 、即時串流，以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需請求、接收指定內容的廣告相關資訊，並分階段將廣告置於內容中。
title: 插入廣告
exl-id: 3a472435-2e37-46d6-8c08-dd6e953c7a7a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 概觀 {#inserting-ads-overview}

廣告插入會解析視訊點播(VOD) 、即時串流，以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需請求、接收指定內容的廣告相關資訊，並分階段將廣告置於內容中。

一個 *`ad break`* 包含一或多個依序播放的廣告。 TVSDK會將廣告插入主要內容，作為一或多個廣告插播的成員。

## 停用前段廣告 {#disable-preroll-ads}

若要停用前置，請變更預設機會產生器，使其不進行前置通話。 預設機會產生器為：

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

若要停用即時資料流上的前段播放，請變更上述設定，使其僅包含SpliceOutOpportunityGenerator：

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
