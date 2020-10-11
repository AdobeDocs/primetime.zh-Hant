---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Primetime 動態廣告插入說明
user-guide-description: Explains how to monetize content by inserting user-targeted dynamic ads on the server and engage audience with personalized ads.
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# Dynamic Ad Insertion Help {#ad-insertion}

+ [動態廣告插入概述](home.md)
+ 開始使用Primetime廣告插入{#get-started}
   + [概觀](get-started-ptai.md)
   + [準備使用Primetime廣告插入](setup-ptai.md)
   + [整合您的廣告伺服器](integrate-ad-server.md)
   + [整合您的CDN](integrate-cdn.md)
   + [在即時／線性串流中使用廣告插入](ad-insertion-live-linear-stream.md)
   + [使用廣告插入VOD](ad-insertion-vod.md)
   + [設定廣告追蹤](set-up-ad-tracking.md)
+ [動態廣告插入發行說明](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [資訊清單伺服器除錯工具](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ 廣告插入資訊清單伺服器API {#manifest-server}
   + [資訊清單伺服器互動概觀](msapi-topics/ms-overview.md)
   + 開始使用Manifest Server {#get-started}
      + [傳送命令至資訊清單伺服器](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [資訊清單伺服器查詢參數](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + 廣告插入請求 {#ad-insert}
      + [廣告插入請求](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [依用戶端和情況選擇的查詢參數](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [促進HLS播放器切換到故障轉移／備份流](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [多位元速率串流](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [部分插入廣告分段](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [CRS廣告傳送的多個CDN支援](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + 取代VOD時間軸 {#replace-vod}
      + [VOD的變更](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [VOD時間軸格式](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [取代VOD時間軸](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + 廣告效果追蹤 {#ad}
      + [廣告追蹤](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [啟用用戶端廣告追蹤](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [非TVSDK用戶端追蹤概觀](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [播放器與資訊清單伺服器互動的API](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [EXT-X-MARKER指令](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookie](msapi-topics/ms-cookies.md)
   + [支援WebVTT標題](msapi-topics/ms-webvtt-captions.md)
   + 檔案格式清單 {#list}
      + [檔案格式](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [用於請求變型資訊清單播放清單之URL的JSON格式](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [追蹤URL的JSON格式](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [用於追蹤URL的VMAP格式](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [視訊播放器需求](msapi-topics/ms-player-req.md)
+ Primetime Creative重新封裝服務 {#crs}
   + [CRS概觀](creative-repackaging-service/crs-overview.md)
   + [CRS的主要用途](creative-repackaging-service/jit-async-hls-conv.md)
   + [多CDN支援](creative-repackaging-service/multi-cdn-supportt.md)
   + [JIT重新封裝的詳細工作流程](creative-repackaging-service/jit-repackage.md)
   + [使用CRS插入ID3計時中繼資料標籤](creative-repackaging-service/inject-id3.md)
   + [重新封裝API](creative-repackaging-service/api-repackage.md)
