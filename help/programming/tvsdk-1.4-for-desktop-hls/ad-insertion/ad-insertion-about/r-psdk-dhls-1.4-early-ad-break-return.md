---
description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
seo-title: 實作早期廣告插播傳回
title: 實作早期廣告插播傳回
uuid: 984b6ed0-c929-49a3-9553-e30d1a7758ed
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 實作早期廣告插播傳回{#implementing-an-early-ad-break-return}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

>[!NOTE] {othertype=&quot;Presequate&quot;}
>
>您必須訂閱剪接／插入廣告標籤( `#EXT-X-CUE-OUT`、 `#EXT-X-CUE-IN`和 `#EXT-X-CUE`)。

以下是需要考慮的一些要求：

* 剖析出現線上 `EXT-X-CUE-IN` 性或FER串流中的標籤（或等效標籤標籤標籤）。

   將標籤註冊為廣告早期返回點的標籤。 在播放 `adBreaks` 期間只播放此標籤位置，這會覆寫由前導標籤 `adBreak` 標籤的持續 `EXE-X-CUE-OUT` 時間。

* 如果同一 `EXT-X-CUE-IN` 個標籤存在兩個 `EXT-X-CUE-OUT` 標籤，則出現的第 `EXT-X-CUE-IN` 一個標籤是計數的標籤。

* 如果標 `EXE-X-CUE-IN` 記顯示在時間軸中，但沒有前 `EXT-X-CUE-OUT` 導標籤，則 `EXE-X-CUE-IN` 標籤將被丟棄。

   在即時串流中，如果 `EXT-X-CUE-OUT` 前導標籤剛移出視窗，TVSDK將不會回應。

* 當廣告插播有提早返回時，會播放 `adBreak` ，直到播放磁頭返回原始位置，當廣告插播應該結束時，再從該位置繼續播放主要內容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 標 `SpliceIn` 記標籤廣告插播的開始和結束。 標籤類型 `SpliceOut` 的持續時 `EXE-X-CUE` 間可能為零，而標籤 `SpliceIn` 類型 `EXE-X-CUE` 會標籤廣告分段的結束。 它們會出現在單一標籤中，並依類型而有所不同。

**一個不同類型的標籤**

例如，以下是一個具有不同類型的標籤：

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

在具有不同類型的單一標籤範例中，如果類型的持 `SpliceOut` 續時間為零，則 `SpliceOut` 和 `SpliceIn` 必須共同處理每個廣告分段。 目前， `SpliceOut` 具有非零持續時間且不需要配對標籤的標籤 `SpliceIn` 較為典型。

**兩個獨立的標籤**

較典型的情景是具 `SpliceOut` 有非零持續時間的標籤，不需要配對標 `SpliceIn` 記。 在這裡，配對標 `SpliceIn` 記會在廣告插播播放期間標籤廣告插播的結尾，但廣告插播會在標籤位置被剪短，而主要內容會在此 `SpliceIn` 位置開始播放。

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

