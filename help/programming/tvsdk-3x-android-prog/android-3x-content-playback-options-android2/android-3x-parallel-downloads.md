---
description: 同時下載視訊和音訊（而非串連）可減少啟動延遲。
title: 平行下載
exl-id: 7cc9afbf-e495-40b0-a8ff-86d4939d1b15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 平行下載 {#parallel-downloads}

同時下載視訊和音訊（而非串連）可減少啟動延遲。

平行下載可播放隨選影片(VOD)檔案、最佳化伺服器的可用頻寬使用量、降低進入緩衝區執行不足的機率，以及將下載和播放之間的延遲降至最低。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

若沒有平行下載，TVSDK會向視訊區段發出請求，而在視訊區段載入後，它會請求一或兩個音訊區段。 透過平行下載，音訊和視訊區段會同時下載，而非依序下載。 此外，由於每個區段有兩個連線和兩個HTTP請求並行，因此資料到達熒幕的速度會更快。

>[!NOTE]
>
>此功能僅適用於將音訊和視訊編碼為不同檔案（未混合的內容）的內容，而不適用於MP4內容，MP4內容一律混合在一起。 HLS內容通常會取消混音，尤其是使用替代音訊時。

<!-- 

See comment above (DASH use case removed).

  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

HTTP連線可能會在以下階段遇到延遲：

* 建立與伺服器的TCP/IP連線時

   雖然使用者端和伺服器已同意通訊，但尚未發生HTTP通訊。 這種延遲型別取決於使用者端和伺服器之間的基礎結構。 此程式需要找到使用者端與伺服器之間的網際網路路徑，並確保路由上的所有裝置（例如路由器和防火牆）都同意資料傳輸。
* 透過TCP/IP連線傳送區段或資訊清單的HTTP要求時。

   伺服器會接收請求、處理請求，然後開始將資料傳回使用者端。 延遲的程度取決於伺服器上軟體的負載和複雜性，並且在某種程度上取決於使用者端傳送請求時的上傳連線速度。
