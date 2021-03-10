---
description: 對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。
title: 即時／線性廣告解析與插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 即時／線性廣告解析與插入{#live-linear-ad-resolving-and-insertion}

對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。

在播放前及播放期間，TVSDK會解析已知廣告、以相同持續時間的廣告插播取代部分主要內容，並視需要重新計算虛擬時間軸。 廣告分段的位置由資訊清單所定義的提示點指定。

TVSDK會以下列方式插入廣告：

* **前置**，內容開始時。
* **中段**，在內容中間。

即使持續時間長於或短於提示點取代持續時間，TVSDK仍接受廣告插播。 依預設，TVSDK支援`#EXT-X-CUE`提示作為解析和放置廣告時的有效廣告標籤。 此標籤需要以秒為單位的中繼資料欄位`DURATION`和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義並訂閱其他提示（標籤）。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 TVSDK可解析任何新廣告，並在資訊清單中定義的即時或線性串流中遇到提示點時插入廣告。 廣告解析並插入後，TVSDK會再次計算虛擬時間軸並調度`TimelineItemsUpdatedEventListener.onTimelineUpdated`事件。
