---
title: 促進HLS播放器切換到容錯移轉/備份資料流
description: 如果無法擷取主要集的任何資料流，Apple HLS棧疊支援切換到容錯移轉/備份資料流。 對於Apple HLS裝置，為了促進容錯移轉，您可以發出訊號給資訊清單伺服器，將主播放清單中識別的主要和容錯移轉資料流視為中斷連線的集合（具有自己的UUID）。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 促進HLS播放器切換到容錯移轉/備份資料流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果無法擷取主要集的任何資料流，Apple HLS棧疊支援切換到容錯移轉/備份資料流。 對於Apple HLS裝置，為了促進容錯移轉，您可以發出訊號給資訊清單伺服器，將主播放清單中識別的主要和容錯移轉資料流視為中斷連線的集合（具有自己的UUID）。

若要促進切換至Apple HLS裝置上的容錯移轉或備份資料流，您可以指定 `ptfailover` BootstrapURL中的引數。 如果您提供此引數，資訊清單伺服器將為每個容錯移轉集建立個別的播放工作階段（決定拼接的廣告）。

## 詳細資料

當您包含時，SSAI如何處理HLS切換到容錯移轉/備份 `ptfailover=true` 在Bootstrap請求中：

* 當主播放清單包含主要和備份集時：

   * 資訊清單伺服器會使用識別不同容錯移轉集的AV串流URL。 `BANDWIDTH` 屬性和AV串流URL的剖析順序。 它會建立個別的內部播放工作階段（由不同的UUID識別），並建立指向資訊清單伺服器的串流URL，這些UUID可識別不同的播放工作階段。
   * 資訊清單伺服器會使用相符專案識別不同容錯移轉集的I-Frame資料流URL `RESOLUTION` 屬性和I-Frame串流URL的剖析順序。 SSAI會使用UUID來識別指向SSAI的I-Frame資料流URL之相關AV資料流。
   * 對於此功能，資訊清單伺服器僅支援 `EXT-X-MEDIA` 沒有URI屬性的群組。
   * 資訊清單伺服器偵測來自CDN的404錯誤回應，其中包含 `X-Object-Too-Old: true` 標頭，並在將回應傳送至播放器時保留狀態代碼和標頭。

* 前段廣告只會新增至主要集；在容錯移轉集中會完全停用前段廣告，以避免播放器切換至容錯移轉資料流時有任何錯誤和/或重複的前段廣告。
