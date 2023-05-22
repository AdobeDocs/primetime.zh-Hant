---
description: 對於即時/線性內容，瀏覽器TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。
title: 即時/線性廣告解析和插入
exl-id: 5d5954c6-9d1c-4900-9813-d3248fd61911
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 即時/線性廣告解析和插入{#live-linear-ad-resolving-and-insertion}

對於即時/線性內容，瀏覽器TVSDK用相同持續時間的廣告中斷替換主流內容的塊，以使時間線持續時間保持相同。

在播放之前和播放期間，瀏覽器TVSDK解析已知廣告，用相同持續時間的廣告分段替換部分主內容，並在必要時重新計算虛擬時間軸。 廣告斷點的位置由清單定義的提示點指定。

瀏覽器TVSDK以下列方式插入廣告：

* **預卷**，位於內容的開頭。

即使持續時間長於或短於提示點替換持續時間，瀏覽器TVSDK也會接受廣告中斷。 預設情況下，瀏覽器TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時提示作為有效的廣告標籤。 此標籤需要元資料欄位 `DURATION` 以秒為單位，提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義和訂閱附加提示（標籤）。

播放開始後，視頻引擎定期刷新清單檔案。 瀏覽器TVSDK解析任何新廣告，並在清單中定義的即時或線性流中遇到提示點時插入廣告。 在解析和插入廣告後，瀏覽器TVSDK再次計算虛擬時間軸並調度 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` 的子菜單。

>[!TIP]
>
>對於即時流，Browser TVSDK僅支援MP4和HLS卷前和中卷廣告。
