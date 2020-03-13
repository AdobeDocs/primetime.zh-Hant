---
description: 對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。
seo-description: 對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。
seo-title: 解析並插入即時／線性廣告
title: 解析並插入即時／線性廣告
uuid: 722569f2-d260-4fcc-b6b9-01d86aa00e28
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 解析並插入即時／線性廣告 {#resolve-and-insert-live-linear-ad}

對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。

在播放前及播放期間，TVSDK會解析已知廣告、以相同持續時間的廣告插播取代部分主要內容，並視需要重新計算虛擬時間軸。 廣告分段的位置由資訊清單所定義的提示點指定。

TVSDK會以下列方式插入廣告：

* **前置卷**，會置於內容之前。
* **Mid-roll**，它位於內容的中間。

即使持續時間長於或短於提示點取代持續時間，TVSDK仍接受廣告插播。 依預設，TVSDK支援在解析 `#EXT-X-CUE` 和放置廣告時，提示為有效的廣告標籤。 此標籤需要以秒 `DURATION` 表示中繼資料欄位值，以及提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義並訂閱其他提示（標籤）。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 TVSDK可解析任何新廣告，並在資訊清單中定義的即時或線性串流中遇到提示點時插入廣告。 在解析並插入廣告後，TVSDK會再次計算虛擬時間軸，並調度事 `TimelineItemsUpdatedEventListener.onTimelineUpdated` 件。