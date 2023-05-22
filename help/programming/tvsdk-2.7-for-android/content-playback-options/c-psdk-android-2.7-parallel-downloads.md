---
description: 並行下載視頻和音頻，而不是串列下載，可減少啟動延遲。
title: 並行下載
exl-id: 6c93154b-8de4-448b-bc33-776fcc1f6243
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 並行下載 {#parallel-downloads}

並行下載視頻和音頻，而不是串列下載，可減少啟動延遲。

並行下載允許播放視頻點播(VOD)檔案，優化伺服器的可用頻寬使用，降低進入緩衝區運行不足情況的可能性，並最小化下載和回放之間的延遲。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

如果沒有並行下載，TVSDK會發出對視頻段的請求，並且在載入視頻段後，它會請求一個或兩個音頻段。 通過並行下載，音頻和視頻段可同時下載，而不是按順序下載。 此外，由於每個段有兩個連接和兩個HTTP請求並行，因此資料到達螢幕的速度更快。

>[!NOTE]
>
>此功能僅適用於音頻和視頻被編碼為不同檔案（未混合內容）的內容，不適用於MP4內容，MP4內容總是被混合。 HLS內容通常被解壓縮，特別是使用備用音頻。

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP連接可能在以下階段遇到延遲：

* 在建立與伺服器的TCP/IP連接時

   雖然客戶端和伺服器已同意通信，但尚未發生HTTP通信。 這種類型的延遲取決於客戶端和伺服器之間的基礎架構。 此過程要求在客戶端和伺服器之間查找通過Internet的路徑，並確保路由上的所有設備（如路由器和防火牆）都同意資料傳輸。
* 通過TCP/IP連接發送段或清單的HTTP請求時。

   伺服器接收請求，處理請求，並開始將資料發回給客戶端。 延遲程度取決於伺服器上的軟體負載和複雜性，在客戶端發送請求時，還在某種程度上取決於上載連接速度。
