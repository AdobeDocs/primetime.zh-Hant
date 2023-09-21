---
description: 廣告插入會解析視訊點播(VOD)、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。
title: 插入廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# 概觀 {#insert-ads-overview}

廣告插入會解析視訊點播(VOD)、即時串流以及使用廣告追蹤和廣告播放的線性串流的廣告。 TVSDK會向廣告伺服器提出必要要求、接收指定內容之廣告的相關資訊，並分階段將廣告置於內容中。

廣告插播包含一或多個循序播放的廣告。 TVSDK會將廣告插入主要內容，作為一或多個廣告插播的成員。

>[!TIP]
>
>如果廣告發生錯誤，TVSDK會忽略廣告。
