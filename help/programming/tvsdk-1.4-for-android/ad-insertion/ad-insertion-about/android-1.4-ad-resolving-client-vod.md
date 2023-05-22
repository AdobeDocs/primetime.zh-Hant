---
description: 對於視頻點播(VOD)內容，TVSDK通過在主內容中拼接廣告來插入廣告斷點，從而時間線持續時間增加。
title: 視頻點播廣告解析和插入
exl-id: 2e45fc35-85ca-4e34-b300-cf65878eeac6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 視頻點播廣告解析和插入{#vod-ad-resolving-and-insertion}

對於視頻點播(VOD)內容，TVSDK通過在主內容中拼接廣告來插入廣告斷點，從而時間線持續時間增加。

在回放之前，TVSDK解析已知廣告，按照從Adobe Primetime廣告決策返回的時間軸所述在主要內容中插入廣告中斷，並在必要時重新計算虛擬時間軸。

TVSDK以下列方式插入廣告：

* **預卷**，位於內容之前。
* **中間卷**&#x200B;的子菜單。
* **後滾**，位於內容之後。

播放開始後，內容中不會發生其他更改。 廣告不能是：

* 已插入
* 已刪除

   例如，您不能從內容中刪除內置廣告，以提供無廣告體驗。
* 已更換

   例如，不能用定向廣告替換內置廣告。
