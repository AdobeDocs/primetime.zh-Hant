---
description: 如果Apple HLS堆棧無法檢索主集的任何流，則支援切換到故障切換／備份流。 對於Apple HLS裝置，為方便進行容錯，您可以傳訊manifest伺服器，將主播放清單中識別的主要和容錯串流視為分離集（使用其本身的UUID）。
seo-description: 如果Apple HLS堆棧無法檢索主集的任何流，則支援切換到故障切換／備份流。 對於Apple HLS裝置，為方便進行容錯，您可以傳訊manifest伺服器，將主播放清單中識別的主要和容錯串流視為分離集（使用其本身的UUID）。
seo-title: 促進HLS播放器切換到故障轉移／備份流
title: 促進HLS播放器切換到故障轉移／備份流
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# 促進HLS播放器切換到故障轉移／備份流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果Apple HLS堆棧無法檢索主集的任何流，則支援切換到故障切換／備份流。 對於Apple HLS裝置，為方便進行容錯，您可以傳訊manifest伺服器，將主播放清單中識別的主要和容錯串流視為分離集（使用其本身的UUID）。

為方便在Apple HLS裝置上切換至容錯移轉或備份串流，您可以在引導程 `ptfailover` 式URL中指定參數。 如果您提供此參數，資訊清單伺服器會針對每個容錯移轉集建立個別的播放工作階段（決定銜接的廣告）。

## 詳細資訊

在Bootstrap請求中包含時，SSAI如何處理HLS切換到故障 `ptfailover=true` 轉移／備份的操作：

* 當主播放清單包含主要和備份集時：

   * 資訊清單伺服器使用屬性和AV串流URL的解析順序，來識 `BANDWIDTH` 別不同故障切換集的AV串流URL。 它會建立個別的內部播放作業（由個別的UUID識別），並建立指向資訊清單伺服器的串流URL，其中不同的UUID會識別不同的播放作業。
   * 資訊清單伺服器使用相符屬性和I-Frame串流URL的解析順序，來識 `RESOLUTION` 別不同故障切換集的I-Frame串流URL。 SSAI使用UUID來識別指向SSAI的I-Frame串流URL的相關AV串流。
   * 對於此功能，資訊清單伺服器僅支援主播 `EXT-X-MEDIA` 清單中不含URI屬性的群組。
   * 資訊清單伺服器偵測來自具有標題的CDN的404錯誤回應 `X-Object-Too-Old: true` ，並在傳送該回應給播放器時保留狀態碼和標題。

* 前段廣告只添加到主集；在故障切換集中完全禁用它們，以避免當播放器切換到故障切換流時出現任何錯誤和／或重複的前滾廣告。

