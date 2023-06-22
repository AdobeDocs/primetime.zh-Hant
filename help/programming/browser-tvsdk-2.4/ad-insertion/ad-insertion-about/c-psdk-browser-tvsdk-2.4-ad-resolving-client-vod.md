---
description: 針對隨選影片(VOD)內容，瀏覽器TVSDK會將廣告拼接在主要內容中，藉此插入廣告插播，讓時間軸持續時間增加。
title: VOD廣告解析和插入
exl-id: c2a2f14b-c90d-47fc-9dcc-eff8b1491dde
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

針對隨選影片(VOD)內容，瀏覽器TVSDK會將廣告拼接在主要內容中，藉此插入廣告插播，讓時間軸持續時間增加。

在播放之前，瀏覽器TVSDK會解析已知廣告、依照Adobe Primetime ad decisioning傳回之時間軸的說明在主要內容中插入廣告插播，並在必要時重新計算虛擬時間軸。

瀏覽器TVSDK會以下列方式插入廣告：

* **前置滾動**，即內容之前。
* **後置滾動**，在內容之後。

播放開始後，內容中不會發生其他變更。 廣告不可為：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告以提供無廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。
