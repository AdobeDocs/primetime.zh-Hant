---
description: 您可以使用名為「播放」的廣告和內容段的格式化清單來指定或覆蓋視頻點播內容中廣告中斷的時間線。
title: VOD時間線格式
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# VOD時間線格式 {#vod-timeline-format}

您可以使用名為「播放」的廣告和內容段的格式化清單來指定或覆蓋視頻點播內容中廣告中斷的時間線。

## 莢 {#section_606E9456E25E41C8B8537A023DDD96CE}

Pod是廣告片段或內容片段。 時間軸由包序列組成，用分號分隔。 存在以下類型的莢：

### 廣告分段

```
B,duration,maximum_number_of_ads,position
```

持續時間以秒為單位，精度為0.001（毫秒）;廣告數是整數。 職位是以下之一：* **n** 無 — 無廣告* **p** 預滾動 — 內容之前* **米** 中間卷 — 內容內* **t** 後滾動 — 內容後

比如說， `B,60,2,p` 代表在內容之前最多2個廣告的1分鐘休息時間。

### 內容段 — 章

```
C,duration,number_of_lots
```

持續時間以秒為單位，精度為0.001（毫秒）;批次數（內容的部分）是整數。 比如說， `C,300,1` 代表一個五分鐘的內容。