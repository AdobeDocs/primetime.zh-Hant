---
description: 對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。
seo-description: 對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。
seo-title: 即時／線性廣告解析與插入
title: 即時／線性廣告解析與插入
uuid: 69f287aa-b707-442b-8e07-16f81b242c4b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 即時／線性廣告解析與插入{#live-linear-ad-resolving-and-insertion}

對於即時／線性內容，TVSDK會以相同持續時間的廣告分段來取代主串流內容區塊，如此時間軸持續時間就會維持不變。

在播放前及播放期間，TVSDK會解析已知廣告、以相同持續時間的廣告插播取代部分主要內容，並視需要重新計算虛擬時間軸。 廣告分段的位置由資訊清單所定義的提示點指定。

TVSDK會以下列方式插入廣告：

* **Pre-roll**，此為內容的開頭。
* **Mid-roll**，位於內容中間。

即使持續時間長於或短於提示點取代持續時間，TVSDK仍接受廣告插播。 依預設，TVSDK支援在解析 `#EXT-X-CUE` 和放置廣告時，提示為有效的廣告標籤。 此標籤需要以秒為單位 `DURATION` 的中繼資料欄位和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>在執行慣 `AdPolicySelector`例時，可以針對中的前滾、中滾和後滾給 `AdBreakTimelineItem``AdPolicyInfo`不同的策略，該策略基於s的類 `AdBreakTimelineItem`型。例如，您可以在播放中段內容後保留該內容，但在播放後移除前段內容。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 TVSDK可解析任何新廣告，並在資訊清單中定義的即時或線性串流中遇到提示點時插入廣告。 在解析並插入廣告後，TVSDK會再次計算虛擬時間軸，並調度事 `TimelineEvent.TIMELINE_UPDATED` 件。
