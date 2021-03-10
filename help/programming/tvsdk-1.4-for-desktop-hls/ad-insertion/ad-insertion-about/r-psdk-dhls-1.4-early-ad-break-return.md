---
description: 若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。
title: 實作早期廣告插播傳回
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# 實作早期廣告插播傳回{#implementing-an-early-ad-break-return}

若是即時串流廣告插入，您可能需要先退出廣告插播，才能播放該插播中的所有廣告。

>[!NOTE]
>
>您必須訂閱剪接出／插入廣告標籤（`#EXT-X-CUE-OUT`、`#EXT-X-CUE-IN`和`#EXT-X-CUE`）。

以下是需要考慮的一些要求：

* 剖析出現線上性或FER串流中的標籤，例如`EXT-X-CUE-IN`（或等效標籤標籤標籤）。

   將標籤註冊為廣告早期返回點的標籤。 在播放期間，只播放`adBreaks`，直到此標籤位置覆寫由前導`EXE-X-CUE-OUT`標籤標籤的`adBreak`的持續時間。

* 如果同一個`EXT-X-CUE-OUT`標籤存在兩個`EXT-X-CUE-IN`標籤，則顯示的第一個`EXT-X-CUE-IN`標籤是計數的標籤。

* 如果`EXE-X-CUE-IN`標籤出現在時間軸中，但沒有前導`EXT-X-CUE-OUT`標籤，則會捨棄`EXE-X-CUE-IN`標籤。

   在即時串流中，如果前導`EXT-X-CUE-OUT`標籤剛從視窗移出，TVSDK將不會回應。

* 當廣告插播有提早返回時，`adBreak`會播放，直到播放磁頭返回原本的位置（廣告插播應該結束時），並從該位置繼續播放主要內容。

## SpliceOut和SpliceIn {#section_36DD55BA58084E21BD3DC039BB245C82}

`SpliceOut` 標 `SpliceIn` 記標籤廣告分段的開始和結束。`EXE-X-CUE`標籤的`SpliceOut`類型的持續時間可能為零，而`SpliceIn`類型的`EXE-X-CUE`標籤會標籤廣告分隔的結束。 它們會出現在單一標籤中，並依類型而有所不同。

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

在不同類型的一個標籤範例中，如果`SpliceOut`類型的持續時間為零，則`SpliceOut`和`SpliceIn`必須共同處理每個廣告分段。 目前，`SpliceOut`標籤具有非零持續時間且不需要配對`SpliceIn`標籤較典型。

**兩個獨立的標籤**

較典型的情況是具有非零持續時間的`SpliceOut`標籤，且不需要配對`SpliceIn`標籤。 在這裡，配對`SpliceIn`標籤會在廣告插播播放期間標籤廣告插播的結尾，但廣告插播會在`SpliceIn`標籤位置被剪短，而主要內容會在此位置開始播放。

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

