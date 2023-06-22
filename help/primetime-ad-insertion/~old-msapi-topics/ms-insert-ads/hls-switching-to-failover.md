---
description: 如果無法擷取主要集的任何資料流，Apple HLS棧疊支援切換至容錯移轉/備份資料流。 對於Apple HLS裝置，為了方便容錯移轉，您可以傳送訊號給資訊清單伺服器，以將主要播放清單中識別的主要和容錯移轉資料流視為脫離連線的集合（使用其自己的UUID）。
title: 促進HLS播放器切換到容錯移轉/備份資料流
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 促進HLS播放器切換到容錯移轉/備份資料流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果無法擷取主要集的任何資料流，Apple HLS棧疊支援切換至容錯移轉/備份資料流。 對於Apple HLS裝置，為了方便容錯移轉，您可以傳送訊號給資訊清單伺服器，以將主要播放清單中識別的主要和容錯移轉資料流視為脫離連線的集合（使用其自己的UUID）。

若要加速切換至Apple HLS裝置上的容錯移轉或備份資料流，您可以指定 `ptfailover` BootstrapURL中的引數。 如果您提供此引數，資訊清單伺服器會為每個容錯移轉集建立個別的播放工作階段（決定拼接的廣告）。

## 詳細資料

當您包含時，SSAI如何處理HLS切換到容錯移轉/備份 `ptfailover=true` 在Bootstrap請求中：

* 當主要播放清單包含主要和備份集時：

   * 資訊清單伺服器會使用識別不同容錯移轉集的AV資料流URL。 `BANDWIDTH` 屬性和AV資料流URL的剖析順序。 它會建立個別的內部播放工作階段（以個別的UUID識別），並建立指向資訊清單伺服器的串流URL，這些UUID會識別不同的播放工作階段。
   * 資訊清單伺服器會使用相符專案來識別不同容錯移轉集的I-Frame資料流URL `RESOLUTION` I-Frame資料流URL的屬性和剖析順序。 SSAI會使用識別I-Frame串流URL相關AV串流的UUID，指向SSAI。
   * 對於此功能，資訊清單伺服器僅支援 `EXT-X-MEDIA` 群組在主播放清單中沒有URI屬性。
   * 資訊清單伺服器會偵測來自CDN的404錯誤回應，其中包含 `X-Object-Too-Old: true` 標題，並在將該回應傳送至播放器時保留狀態代碼和標題。

* 前段廣告只會新增到主要集；在容錯移轉集中會完全停用前段廣告，以避免播放器切換至容錯移轉資料流時有任何錯誤和/或重複的前段廣告。

