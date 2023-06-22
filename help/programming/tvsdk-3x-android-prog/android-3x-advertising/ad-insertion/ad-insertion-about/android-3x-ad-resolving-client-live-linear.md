---
description: 對於即時/線性內容，TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。
title: 解析和插入即時/線性廣告
exl-id: 2097520f-283b-4839-af5e-b1cfb0f3f359
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 解析和插入即時/線性廣告 {#resolve-and-insert-live-linear-ad}

對於即時/線性內容，TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。

在播放之前和期間，TVSDK會解析已知廣告、以相同持續時間的廣告插播取代主要內容的部分，並在必要時重新計算虛擬時間軸。 廣告插播的位置由資訊清單定義的提示點指定。

TVSDK會以下列方式插入廣告：

* **前置滾動**，會放在內容之前。
* **中間滾動**，會放置在內容的中間。

即使持續時間長於或短於提示點取代持續時間，TVSDK也會接受廣告插播。 根據預設，TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時，提示為有效的廣告標籤。 此標籤需要中繼資料欄位 `DURATION` 要以秒為單位表示的值，以及提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義並訂閱其他提示（標籤）。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 TVSDK會解析任何新廣告，並在資訊清單中定義的即時或線性資料流中遇到提示點時插入廣告。 解析並插入廣告後，TVSDK會再次計算虛擬時間軸，並傳送 `TimelineItemsUpdatedEventListener.onTimelineUpdated` 事件。
