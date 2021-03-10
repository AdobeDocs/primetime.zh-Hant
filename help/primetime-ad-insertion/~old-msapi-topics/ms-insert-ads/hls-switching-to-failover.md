---
description: 如果Apple HLS堆棧無法檢索主集的任何流，則支援切換到故障切換／備份流。 對於Apple HLS裝置，為方便進行容錯，您可以傳訊manifest伺服器，將主播放清單中識別的主要和容錯串流視為分離集（使用其本身的UUID）。
title: 促進HLS播放器切換到故障轉移／備份流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 促進HLS播放器切換到故障切換／備份流{#facilitating-hls-player-switching-to-failover-backup-streams}

如果Apple HLS堆棧無法檢索主集的任何流，則支援切換到故障切換／備份流。 對於Apple HLS裝置，為方便進行容錯，您可以傳訊manifest伺服器，將主播放清單中識別的主要和容錯串流視為分離集（使用其本身的UUID）。

為方便切換至Apple HLS裝置上的容錯移轉或備份串流，您可在BootstrapURL中指定`ptfailover`參數。 如果您提供此參數，資訊清單伺服器會針對每個容錯移轉集建立個別的播放工作階段（決定銜接的廣告）。

## 詳細資訊

在Bootstrap請求中包含`ptfailover=true`時，SSAI如何處理HLS切換到故障切換／備份：

* 當主播放清單包含主要和備份集時：

   * 資訊清單伺服器使用`BANDWIDTH`屬性和AV串流URL的解析順序，識別不同容錯集的AV串流URL。 它會建立個別的內部播放作業（由個別的UUID識別），並建立指向資訊清單伺服器的串流URL，其中不同的UUID會識別不同的播放作業。
   * 資訊清單伺服器使用相符的`RESOLUTION`屬性和I-Frame串流URL的解析順序，來識別不同容錯集的I-Frame串流URL。 SSAI使用UUID來識別指向SSAI的I-Frame串流URL的相關AV串流。
   * 對於此功能，資訊清單伺服器僅支援主播放清單中不含URI屬性的`EXT-X-MEDIA`群組。
   * 資訊清單伺服器偵測來自具有`X-Object-Too-Old: true`標題的CDN的404錯誤回應，並在傳送該回應給播放器時保留狀態碼和標題。

* 前段廣告只添加到主集；在故障切換集中完全禁用它們，以避免當播放器切換到故障切換流時出現任何錯誤和／或重複的前滾廣告。

