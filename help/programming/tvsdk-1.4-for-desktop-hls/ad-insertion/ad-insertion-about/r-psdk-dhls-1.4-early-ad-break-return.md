---
description: 對於直播串流廣告插入，您可能需要從廣告插播結束，然後播放插播中的所有廣告直到完成。
title: 實作提早的廣告插播回報
exl-id: 584e870e-1408-41a9-bb6f-e82b921fe99e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 實作提早的廣告插播回報{#implementing-an-early-ad-break-return}

對於直播串流廣告插入，您可能需要從廣告插播結束，然後播放插播中的所有廣告直到完成。

>[!NOTE]
>
>您必須訂閱接合退出/加入廣告標籤( `#EXT-X-CUE-OUT`， `#EXT-X-CUE-IN`、和 `#EXT-X-CUE`)。

以下是需要考量的一些需求：

* 剖析標籤，例如 `EXT-X-CUE-IN` 線性或FER資料流中出現的（或等效標籤標籤）。

   將標籤註冊為廣告提前回訪點的標籤。 僅播放 `adBreaks` 直到播放期間此標籤位置為止，這會覆寫持續的 `adBreak` 以開頭標籤 `EXE-X-CUE-OUT` 標籤。

* 若為兩個 `EXT-X-CUE-IN` 相同專案有相同的標籤 `EXT-X-CUE-OUT` 標籤，第一個 `EXT-X-CUE-IN` 出現的標籤即會計數。

* 如果 `EXE-X-CUE-IN` 標籤會出現在時間軸中，且沒有行距 `EXT-X-CUE-OUT` 標籤， `EXE-X-CUE-IN` 會捨棄標籤。

   在即時資料流中，如果 `EXT-X-CUE-OUT` 標籤已移出視窗，TVSDK不會回應。

* 當廣告插播提前傳回時， `adBreak` 播放直到播放點回到原本應結束廣告插播的原始位置，並從該位置繼續播放主要內容為止。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 和 `SpliceIn` 標籤會標籤廣告插播的開始和結束。 持續期間 `SpliceOut` 型別 `EXE-X-CUE` 標籤可能是零，而且 `SpliceIn` 型別 `EXE-X-CUE` 標籤會標籤廣告插播的結尾。 它們會出現在同一個標籤中，並依型別而有所不同。

**一個標籤包含不同的型別**

例如，以下是一個具有不同型別的標籤：

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

在具有不同型別的單一標籤中，例如，如果 `SpliceOut` type為0， `SpliceOut` 和 `SpliceIn` 每次廣告插播都必須搭配使用。 目前， `SpliceOut` 持續期間非零的標籤，且不需要配對 `SpliceIn` 標籤較為典型。

**兩個不同的標籤**

較典型的案例是 `SpliceOut` 持續期間非零的標籤，且不需要配對 `SpliceIn` 標籤。 在這裡，進行配對 `SpliceIn` marker會在廣告插播播放期間標籤廣告插播的結尾，但廣告插播會在 `SpliceIn` 標籤位置，主要內容就會開始在此位置播放。

例如，以下是兩個不同的標籤：

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
