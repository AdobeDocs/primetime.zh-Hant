---
description: 對於即時/線性內容，TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。
title: 即時/線性廣告解析和插入
exl-id: b0fbdddf-8529-4f7a-aef2-1764320307f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 即時/線性廣告解析和插入{#live-linear-ad-resolving-and-insertion}

對於即時/線性內容，TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。

在播放之前和期間，TVSDK會解析已知廣告、以相同持續時間的廣告插播取代主要內容的部分，並在必要時重新計算虛擬時間軸。 廣告插播的位置由資訊清單定義的提示點指定。

TVSDK會以下列方式插入廣告：

* **前置滾動**，位於內容的開頭。
* **中間滾動**，位於內容中間。

即使持續時間長於或短於提示點取代持續時間，TVSDK也會接受廣告插播。 根據預設，TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時，提示為有效的廣告標籤。 此標籤需要中繼資料欄位 `DURATION` 秒數和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>實作習慣時 `AdPolicySelector`，可為前段、中段和後段提供不同的原則 `AdBreakTimelineItem`s in `AdPolicyInfo`，此欄位是根據 `AdBreakTimelineItem`s。例如，您可以在播放中段內容後保留該內容，但在播放前段內容後將其移除。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 TVSDK會解析任何新廣告，並在資訊清單中定義的即時或線性資料流中遇到提示點時插入廣告。 解析並插入廣告後，TVSDK會再次計算虛擬時間軸，並傳送 `TimelineEvent.TIMELINE_UPDATED` 事件。
