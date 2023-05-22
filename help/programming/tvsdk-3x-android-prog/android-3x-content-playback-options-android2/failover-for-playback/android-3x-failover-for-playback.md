---
description: 通過Internet流傳輸需要一個穩定的連接來播放來自遠程伺服器的流。 但是，觀眾的Internet連接或流播放的可變性意味著遠程播放可能沒有本地播放的媒體質量。
title: 播放和故障切換
exl-id: ba8326ba-4ff1-46ad-bd18-9c83147ab619
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 概述 {#playback-and-failover-overview}

通過Internet流傳輸需要一個穩定的連接來播放來自遠程伺服器的流。 但是，觀眾的Internet連接或流播放的可變性意味著遠程播放可能沒有本地播放的媒體質量。

>[!IMPORTANT]
>
>黃金時段無法防止ISP中斷或電纜斷線等故障。

黃金時段流提供故障切換保護，以保護回放免受某些遠程伺服器故障或操作故障的影響，從而提供更好的觀看體驗。 儘管存在傳輸問題，TVSDK仍實施故障轉移保護，以最大限度地減少回放中斷並實現無縫回放。 當整個格式副本或片段不可用時，視頻播放器自動切換到備份媒體集。
