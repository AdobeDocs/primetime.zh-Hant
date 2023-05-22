---
description: 廣告插入解析用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。
title: 插入廣告
exl-id: 899d28b5-92aa-42cb-b7e8-9168fb68dbbd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 概述 {#insert-ads-overview}

廣告插入解析用於視頻點播(VOD)、用於即時流媒體以及用於帶有廣告跟蹤和廣告播放的線性流媒體的廣告。 TVSDK向廣告伺服器發出所需請求，接收有關指定內容的廣告資訊，並將廣告分階段放在內容中。

安 *`ad break`* 包含一個或多個按順序播放的廣告。 TVSDK將廣告作為一個或多個廣告分段的成員插入主內容中。

>[!NOTE]
>
>如果廣告有錯誤，TVSDK將忽略該廣告。
