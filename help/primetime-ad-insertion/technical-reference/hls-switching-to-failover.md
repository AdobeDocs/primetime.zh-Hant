---
title: 方便HLS播放器切換到故障切換/備份流
description: AppleHLS堆棧支援在無法檢索主集的任何流時切換到故障切換/備份流。 對於AppleHLS設備，為了便於故障切換，您可以向清單伺服器發出信號，以將主播放清單中標識的主流和故障轉移流視為不連接集（使用它們自己的UUID）。
exl-id: 58c7a490-403f-41b2-bdbd-6f93e27083b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 方便HLS播放器切換到故障切換/備份流 {#facilitating-hls-player-switching-to-failover-backup-streams}

AppleHLS堆棧支援在無法檢索主集的任何流時切換到故障切換/備份流。 對於AppleHLS設備，為了便於故障切換，您可以向清單伺服器發出信號，以將主播放清單中標識的主流和故障轉移流視為不連接集（使用它們自己的UUID）。

為便於切換到AppleHLS設備上的故障轉移或備份流，可以指定 `ptfailover` 的子菜單。 如果提供此參數，清單伺服器將為每個故障轉移集建立單獨的回放會話（這將決定縫合的廣告）。

## 詳細資訊

SSAI如何處理HLS在包括以下內容時切換到故障轉移/備份 `ptfailover=true` 在Bootstrap請求中：

* 當主播放清單包含主播放清單和備份集時：

   * 清單伺服器使用 `BANDWIDTH` 屬性和AV流URL的解析順序。 它建立獨立的內部回放會話（由單獨的UUID標識），並建立指向具有標識不同回放會話的不同UUID的清單伺服器的流URL。
   * 清單伺服器使用匹配項標識不同故障轉移集的I幀流URL `RESOLUTION` 屬性和I幀流URL的解析順序。 SSAI使用UUID標識指向SSAI的I幀流URL的關聯AV流。
   * 對於此功能，清單伺服器僅支援 `EXT-X-MEDIA` 在主播放清單中沒有URI屬性的組。
   * 清單伺服器檢測來自CDN的404錯誤響應 `X-Object-Too-Old: true` 頭，並在將該響應發送到播放器時保留狀態代碼和頭。

* 預卷廣告只添加到主集；它們在故障轉移集中被完全禁用，以避免在播放器切換到故障轉移流時出現任何錯誤和/或重複的預卷廣告。
