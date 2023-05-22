---
description: 對於視頻點播(VOD)內容，瀏覽器TVSDK通過在主內容中拼接廣告來插入廣告斷點，從而時間線持續時間增加。
title: 視頻點播廣告解析和插入
exl-id: c2a2f14b-c90d-47fc-9dcc-eff8b1491dde
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 視頻點播廣告解析和插入{#vod-ad-resolving-and-insertion}

對於視頻點播(VOD)內容，瀏覽器TVSDK通過在主內容中拼接廣告來插入廣告斷點，從而時間線持續時間增加。

在回放之前，瀏覽器TVSDK解析已知廣告，按照從Adobe Primetime廣告決策返回的時間軸所述，在主內容中插入廣告中斷，並在必要時重新計算虛擬時間軸。

瀏覽器TVSDK以下列方式插入廣告：

* **預卷**，位於內容之前。
* **後滾**，位於內容之後。

播放開始後，內容中不會發生其他更改。 廣告不能是：

* 已插入
* 已刪除

   例如，您不能從內容中刪除內置廣告，以提供無廣告體驗。
* 已更換

   例如，不能用定向廣告替換內置廣告。
