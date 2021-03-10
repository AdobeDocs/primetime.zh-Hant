---
description: 透過網際網路串流需要持續穩定的連線，才能播放來自遠端伺服器的串流。 不過，檢視器的網際網路連線或串流播放的可變性，意味著遠端播放可能沒有本機播放的媒體品質。
title: 播放和容錯
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 概述{#playback-and-failover-overview}

透過網際網路串流需要持續穩定的連線，才能播放來自遠端伺服器的串流。 不過，檢視器的網際網路連線或串流播放的可變性，意味著遠端播放可能沒有本機播放的媒體品質。

>[!IMPORTANT]
>
>Primetime無法防止ISP中斷或電纜斷線等故障。

Primetime串流提供容錯保護，以保護播放不受某些遠端伺服器故障或作業故障的影響，提供更佳的觀賞體驗。 儘管有傳輸問題，TVSDK仍實作容錯移轉保護，將播放中斷降至最低並實現順暢播放。 當整個轉譯或片段無法使用時，視訊播放器會自動切換至備份媒體集。