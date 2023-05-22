---
description: 對於即時流廣告插入，您可能需要先退出廣告分段，然後才能播放該分段中的所有廣告，直到完成。
title: 實現早期廣告中斷返回
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 實現早期廣告中斷返回{#implementing-an-early-ad-break-return}

對於即時流廣告插入，您可能需要先退出廣告分段，然後才能播放該分段中的所有廣告，直到完成。

>[!NOTE]
>
>必須訂閱剪接輸出/插入廣告標籤( `#EXT-X-CUE-OUT`。 `#EXT-X-CUE-IN`, `#EXT-X-CUE`)。

以下是需要考慮的一些要求：

* 分析標籤，如 `EXT-X-CUE-IN` （或等效標籤標籤）。

   將標籤註冊為早期返回點的標籤。 僅播放 `adBreaks` 直到回放期間此標籤位置，這將覆蓋 `adBreak` 標有前導 `EXE-X-CUE-OUT` 標籤。

* 如果是兩個 `EXT-X-CUE-IN` 同一標籤存在 `EXT-X-CUE-OUT` 標籤，第一個 `EXT-X-CUE-IN` 顯示的標籤是計數的標籤。

* 如果 `EXE-X-CUE-IN` 標籤出現在時間軸中，但不帶前導 `EXT-X-CUE-OUT` 標籤， `EXE-X-CUE-IN` 標籤被丟棄。

   在直播流中，如果 `EXT-X-CUE-OUT` 標籤剛從窗口移出，TVSDK將不響應。

* 當廣告時段提前回來時， `adBreak` 播放，直到播放頭返回原始位置，而廣告中斷應該結束，然後從該位置繼續播放主要內容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 和 `SpliceIn` 標籤標籤廣告分段的開始和結束。 持續時間 `SpliceOut` 類型 `EXE-X-CUE` 標籤可能為零，並且 `SpliceIn` 類型 `EXE-X-CUE` 標籤標籤廣告分段的結尾。 它們出現在一個標籤中，並且按類型不同。

**具有不同類型的一個標籤**

例如，下面是一個具有不同類型的標籤：

```
#EXTM3U#EXT-X-TARGETDURATION:10
#EXT-X-VERSION:3
#EXT-X-MEDIA-SEQUENCE:44
  
#EXTINF:9.9,
https://server-host/path/file44.ts
#EXTINF:4.2,
https://server-host/path/file45.ts
  
#EXT-X-CUE:TYPE="SpliceOut",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138",AVAIL-NUM="1",AVAILS-EXPECTED="10"
#EXTINF:5.8,
https://server-host/path/file46.ts
#EXTINF:9.9,
https://server-host/path/file47.ts
...
#EXTINF:9.9,
https://server-host/path/file56.ts
#EXTINF:4.2,
https://server-host/path/file57.ts
#EXT-X-CUE:TYPE="SpliceIn",ID="1",DURATION="0",TIME="266.198",PROGRAM-ID="138"
#EXTINF:9.9,
https://server-host/path/file58.ts
```

在具有不同類型的一個標籤示例中，如果 `SpliceOut` 類型為零， `SpliceOut` 和 `SpliceIn` 每次廣告都必須齊心協力。 當前， `SpliceOut` 具有非零持續時間且不需要配對的標籤 `SpliceIn` 標籤更為典型。

**兩個獨立的標籤**

更典型的情形是 `SpliceOut` 具有非零持續時間且不需要配對的標籤 `SpliceIn` 標籤。 這裡，一對 `SpliceIn` 標籤標籤在播放廣告中斷期間標籤廣告中斷的結束，但廣告中斷在播放 `SpliceIn` 標籤位置，主內容開始在此位置播放。

例如，下面是兩個單獨的標籤：

```
#EXT-X-CUE-OUT:ID=105,DURATION=30.0,TIME=1081.08
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589090425811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589150485811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589210545811,format=m3u8-aapl-v4)
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589270605811,format=m3u8-aapl-v4)
#EXT-X-CUE-IN:ID=105,TIME=1105.104
#EXTINF:6.006000,no-desc
/live/hls/nbc-fer/QualityLevels(2200000)/Fragments(video=14332589330665811,format=m3u8-aapl-v4)
```
