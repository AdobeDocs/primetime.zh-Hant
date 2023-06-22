---
description: 針對隨選影片(VOD)內容，TVSDK會在主要內容中拼接廣告，插入廣告插播，以增加時間軸持續時間。
title: VOD廣告解析和插入
exl-id: 2e45fc35-85ca-4e34-b300-cf65878eeac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# VOD廣告解析和插入{#vod-ad-resolving-and-insertion}

針對隨選影片(VOD)內容，TVSDK會在主要內容中拼接廣告，插入廣告插播，以增加時間軸持續時間。

在播放之前，TVSDK會解析已知廣告、依照Adobe Primetime ad decisioning傳回之時間軸的說明在主要內容中插入廣告插播，並在必要時重新計算虛擬時間軸。

TVSDK會以下列方式插入廣告：

* **前置滾動**，即內容之前。
* **中間滾動**，即位於內容中。
* **後置滾動**，在內容之後。

播放開始後，內容中不會發生其他變更。 廣告不可為：

* 已插入
* 已刪除

   例如，您無法從內容中刪除內建廣告以提供無廣告體驗。
* 已取代

   例如，您無法將內建廣告取代為目標廣告。
