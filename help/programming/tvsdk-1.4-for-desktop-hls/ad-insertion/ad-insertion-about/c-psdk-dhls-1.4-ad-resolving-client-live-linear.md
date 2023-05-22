---
description: 對於即時/線性內容，TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。
title: 即時/線性廣告解析和插入
exl-id: b0fbdddf-8529-4f7a-aef2-1764320307f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 即時/線性廣告解析和插入{#live-linear-ad-resolving-and-insertion}

對於即時/線性內容，TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。

在播放之前和播放期間，TVSDK解析已知廣告，用相同持續時間的廣告中斷替換部分主內容，並在必要時重新計算虛擬時間軸。 廣告斷點的位置由清單定義的提示點指定。

TVSDK以下列方式插入廣告：

* **預卷**，位於內容的開頭。
* **中間卷**，位於內容的中間。

即使持續時間長於或短於提示點替換持續時間，TVSDK也會接受廣告中斷。 預設情況下，TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時提示作為有效的廣告標籤。 此標籤需要元資料欄位 `DURATION` 以秒為單位，提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

>[!IMPORTANT]
>
>執行習慣 `AdPolicySelector`對卷前、卷中和卷後可給出不同的策略 `AdBreakTimelineItem`在 `AdPolicyInfo`，這基於 `AdBreakTimelineItem`s例如，您可以在播放中間卷內容後保留它，但在播放後刪除預卷內容。

播放開始後，視頻引擎定期刷新清單檔案。 TVSDK解析任何新廣告，並在清單中定義的即時或線性流中遇到提示點時插入廣告。 在解析和插入廣告後，TVSDK再次計算虛擬時間軸並調度 `TimelineEvent.TIMELINE_UPDATED` 的子菜單。
