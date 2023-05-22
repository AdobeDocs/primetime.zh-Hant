---
description: 對於即時/線性內容，TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。
title: 解析並插入即時/線性廣告
exl-id: 2fe55c07-54d2-4a8a-a4e1-9e5ccae17ff9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 解析並插入即時/線性廣告 {#resolve-and-insert-live-linear-ad}

對於即時/線性內容，TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。

在播放之前和播放期間，TVSDK解析已知廣告，用相同持續時間的廣告中斷替換部分主內容，並在必要時重新計算虛擬時間軸。 廣告斷點的位置由清單定義的提示點指定。

TVSDK以下列方式插入廣告：

* **預卷**&#x200B;的子菜單。
* **中間卷**&#x200B;的子菜單。

即使持續時間長於或短於提示點替換持續時間，TVSDK也會接受廣告中斷。 預設情況下，TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時提示作為有效的廣告標籤。 此標籤需要元資料欄位 `DURATION` 以秒為單位表示的值和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義和訂閱附加提示（標籤）。

播放開始後，視頻引擎定期刷新清單檔案。 TVSDK解析任何新廣告，並在清單中定義的即時或線性流中遇到提示點時插入廣告。 在解析和插入廣告後，TVSDK再次計算虛擬時間軸並調度 `TimelineItemsUpdatedEventListener.onTimelineUpdated` 的子菜單。
