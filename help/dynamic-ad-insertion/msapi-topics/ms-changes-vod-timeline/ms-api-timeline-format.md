---
description: 您可以使用稱為pod的廣告和內容區段的格式化清單，指定或覆寫VOD內容中廣告插播的時間軸。
seo-description: 您可以使用稱為pod的廣告和內容區段的格式化清單，指定或覆寫VOD內容中廣告插播的時間軸。
seo-title: VOD時間軸格式
title: VOD時間軸格式
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# VOD時間軸格式 {#vod-timeline-format}

您可以使用稱為pod的廣告和內容區段的格式化清單，指定或覆寫VOD內容中廣告插播的時間軸。

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Pod是廣告插播或內容區段。 時間軸由Pod序列組成，以分號分隔。 有下列類型的Pod:

### 廣告插播

```
B,duration,maximum_number_of_ads,position
```

持續時間以秒為單位，精度為。001（毫秒）;廣告數是整數。 職位是下列其中一項：* **n** None — 無廣告* **p** Pre-roll — 內容* **m** Mid-roll — 內容* **t** Post-roll — 在內容之後

例如， `B,60,2,p` 在內容之前，最多可分1分鐘的分段。

### 內容區段——章節

```
C,duration,number_of_lots
```

持續時間以秒為單位，精度為。001（毫秒）;批次數（內容區段）是整數。 例如， `C,300,1` 代表單一5分鐘的內容區段。