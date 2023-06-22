---
description: 對於即時/線性內容，瀏覽器TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。
title: 即時/線性廣告解析和插入
exl-id: 5d5954c6-9d1c-4900-9813-d3248fd61911
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 即時/線性廣告解析和插入{#live-linear-ad-resolving-and-insertion}

對於即時/線性內容，瀏覽器TVSDK會以相同持續時間的廣告插播取代主要串流內容的區塊，讓時間軸持續時間維持不變。

在播放之前和期間，瀏覽器TVSDK會解析已知廣告、以相同持續時間的廣告插播取代主要內容的部分，並在必要時重新計算虛擬時間軸。 廣告插播的位置由資訊清單定義的提示點指定。

瀏覽器TVSDK會以下列方式插入廣告：

* **前置滾動**，位於內容的開頭。

即使持續時間長於或短於提示點取代持續時間，瀏覽器TVSDK也會接受廣告插播。 依預設，瀏覽器TVSDK支援 `#EXT-X-CUE` 解析和放置廣告時，提示為有效的廣告標籤。 此標籤需要中繼資料欄位 `DURATION` 秒數和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定義並訂閱其他提示（標籤）。

播放開始後，視訊引擎會定期重新整理資訊清單檔案。 瀏覽器TVSDK會解析任何新廣告，並在資訊清單中定義的即時或線性資料流中遇到提示點時插入廣告。 解析並插入廣告後，瀏覽器TVSDK會再次計算虛擬時間軸並傳送 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` 事件。

>[!TIP]
>
>對於即時串流，瀏覽器TVSDK僅支援MP4和HLS前段和中段廣告。
