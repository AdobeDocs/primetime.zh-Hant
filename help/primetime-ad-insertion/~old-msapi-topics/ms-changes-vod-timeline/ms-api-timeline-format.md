---
description: 您可以使用稱為pod的廣告和內容區段的格式化清單，指定或覆寫VOD內容中廣告插播的時間軸。
title: VOD時間軸格式
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# VOD時間軸格式{#vod-timeline-format}

您可以使用稱為pod的廣告和內容區段的格式化清單，指定或覆寫VOD內容中廣告插播的時間軸。

## Pod {#section_606E9456E25E41C8B8537A023DDD96CE}

Pod是廣告插播或內容區段。 時間軸由Pod序列組成，以分號分隔。 有下列類型的Pod:

### 廣告插播

```
B,duration,maximum_number_of_ads,position
```

持續時間以秒為單位，精度為。001（毫秒）;廣告數是整數。 職位是下列其中一項：
* **n**無— 無廣告
* **p**前滾— 內容之前
* **m**中間輥— 內容
* **t**&#x200B;滾動後— 在內容之後

例如，`B,60,2,p`代表內容前最多2個廣告的1分鐘間隔。

### 內容區段——章節

```
C,duration,number_of_lots
```

持續時間以秒為單位，精度為。001（毫秒）;批次數（內容區段）是整數。 例如，`C,300,1`代表單一5分鐘的內容區段。