---
description: 出版業者可建立與HLS相容的視訊播放器，可搭配Primetime資訊清單伺服器端和追蹤工作流程運作。 即時串流和隨選視訊(VOD)案例的資訊清單伺服器介面略有不同。
seo-description: 出版業者可建立與HLS相容的視訊播放器，可搭配Primetime資訊清單伺服器端和追蹤工作流程運作。 即時串流和隨選視訊(VOD)案例的資訊清單伺服器介面略有不同。
seo-title: 非TVSDK用戶端追蹤概觀
title: 非TVSDK用戶端追蹤概觀
uuid: fb23be01-3327-443d-82c4-fb0993e7fec1
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 非TVSDK用戶端追蹤概觀 {#overview-of-non-tvsdk-client-side-tracking}

出版業者可建立與HLS相容的視訊播放器，可搭配Primetime資訊清單伺服器端和追蹤工作流程運作。 即時串流和隨選視訊(VOD)案例的資訊清單伺服器介面略有不同。

資訊清單伺服器提供API，讓自訂播放器可請求下列URL，以用於報告廣告追蹤事件：

* 廣告印象
* 廣告四分位數
* 廣告Pod進度
* 內容pod進度

資訊清單伺服器API會假設任何使用它的視訊播放器都符合最低需求。 如需詳 [細資訊，請參閱視訊播放器](../../msapi-topics/ms-player-req.md) 「需求」。

## 用戶端追蹤工作流程 {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. Player從發佈者取得資訊清單伺服器URL。
1. 播放器會附加特定於其廣告插入需求的查詢參數，並傳送HTTP GET要求至產生的引導URL。 引導URL具有以下語法：

   ```
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   
   For example:
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   URL包含傳送命令至資訊清 [單伺服器中所述的元素](../../msapi-topics/ms-getting-started/ms-sending-cmd.md)。

1. 資訊清單伺服器會建立該播放器的作業階段，並產生唯一的作業階段ID。 它會建立新的變型M3U8播放清單URL，並以JSON回應的形式傳回至播放器。 JSON具有下列語法：

   ```
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   
   For example:
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Player會使用JSON回應的URL，從資訊清單伺服器要求新的變型M3U8主播放清單。
1. 資訊清單伺服器會傳回包含串流層級播放清單URL的新變型M3U8，其語法類似下列：

   ```
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   
   For example:
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. 播放器會選擇適當的單位元速率、串流層級資訊清單URL來播放廣告銜接內容。 例如：

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. 資訊清單伺服器傳回串流層級資訊清單，其包含內容與廣告TS區段連結的連結。 例如：

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >播放器選擇串流層級播放清單URL以取得內容串流。 資訊清單伺服器從CDN擷取原始播放清單。 有些編碼器可能會在title屬性中插入其 `#EXTINF` 他詳細資訊，例如：
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   由於資訊清單伺服器無法推斷非標準屬性的含義以修改廣告銜接播放清單，資訊清單伺服器會移除除此標籤中的持續時間資訊以外的所有其他屬性。 有關詳 [細資訊，請參見HLS規範中的](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) DIFF條目。


1. 若要請求追蹤資訊，播放器會針對所選位元速率，將含 `pttrackingposition` 有任何英數字元值的查詢參數附加至串流層級播放清單URL。 例如：

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. 資訊清單伺服器會傳回填入 [JSON](../../msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) 或 [](../../msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) VMAP物件的播放清單檔案，其中包含目前要求之串流層級m3u8檔案的廣告追蹤資料。

   >[!NOTE]
   >
   >如果廣告插入目前要求的串流層級播放清單中，資訊清單伺服器只會產生廣告追蹤物件。 如果播放器播放的播放清單不含插入廣告，資訊清單伺服器會傳回廣告追蹤播放清單請求的HTTP狀態201。 如果播放器對未播放的串流提出廣告追蹤請求，資訊清單伺服器會傳回HTTP狀態500。 例如，如果目前的播放請求是500.m3u8，資訊清單伺服器會針對廣告追蹤請求傳回500.m3u8中的JSON|VMAP。 不過，如果播放器隨後切換串流以播放800.m3u8,500.m3u8中的廣告追蹤資訊會變成無效，導致404錯誤。

   >[!NOTE]
   >
   >資訊清單伺服器會根據引導URL中的 `pttrackingversion` 值來產生廣告追蹤物件。 如果省略 `pttrackingversion` 或具有無效值，則資訊清單伺服器會自動將廣告追蹤資訊填入每個請求的串流 `#EXT-X-MARKER` 層級播放清單中的標籤中。 如需詳 [細資訊，請參閱](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md)。

1. 播放器會在適當的時間針對每個廣告追蹤事件要求每個廣告追蹤URL。

>[!NOTE]
>
>對於即時串流，播放器必須重複步驟6到10，因為Packager會在即時事件的整個期間持續更新播放清單。

當播放視訊時，播放器必須追蹤播放頭位置，並搭配使用此位置與追蹤從Primetime廣告插入所收到的URL。 追蹤URL會依播放開始時的時間偏移分組。 對於每次時間偏移，每個廣告系統都有一個URL，要傳送追蹤資訊。 即時視訊和隨選視訊格式的其他詳細資訊不同。
