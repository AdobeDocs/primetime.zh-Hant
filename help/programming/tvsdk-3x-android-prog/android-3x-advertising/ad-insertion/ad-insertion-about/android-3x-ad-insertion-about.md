---
description: 廣告插入會解析視訊點播(VOD)、直播串流，以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需請求、接收指定內容的廣告相關資訊，並分階段將廣告置於內容中。
title: 插入廣告
exl-id: 899d28b5-92aa-42cb-b7e8-9168fb68dbbd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 概觀 {#insert-ads-overview}

廣告插入會解析視訊點播(VOD)、直播串流，以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出所需請求、接收指定內容的廣告相關資訊，並分階段將廣告置於內容中。

一個 *`ad break`* 包含一或多個依序播放的廣告。 TVSDK會將廣告插入主要內容，作為一或多個廣告插播的成員。

>[!NOTE]
>
>如果廣告發生錯誤，TVSDK會忽略該廣告。
