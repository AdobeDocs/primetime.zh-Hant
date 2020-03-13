---
description: 並行下載視訊和音訊，而非串連下載，可減少啟動延遲。
seo-description: 並行下載視訊和音訊，而非串連下載，可減少啟動延遲。
seo-title: 並行下載
title: 並行下載
uuid: fa3edb50-7c24-433c-bc50-72d6cf73d834
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 並行下載 {#parallel-downloads}

並行下載視訊和音訊，而非串連下載，可減少啟動延遲。

並行下載允許播放隨選視訊(VOD)檔案，最佳化來自伺服器的可用頻寬使用，降低在執行中進入緩衝區的可能性，並將下載與播放之間的延遲降至最低。

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

若未進行平行下載，TVSDK會發出視訊區段的要求，而在載入視訊區段後，會要求一或兩個音訊區段。 透過並行下載，音訊和視訊區段會同時下載，而非依序下載。 此外，由於每個區段有兩個連線和兩個HTTP要求並行，因此資料會更快到達螢幕。

>[!NOTE]
>
>此功能僅適用於將音訊和視訊編碼為不同檔案（未混合內容）的內容，而不適用於MP4內容，因為MP4內容一律是混合內容。 HLS內容通常未經過混音，尤其是使用替代音訊。

<!-- 

See comment above (DASH use case removed).
<note type="restriction">
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
</note>

 -->

HTTP連線可能會在下列階段發生延遲：

* 建立與伺服器的TCP/IP連接時

   雖然客戶端和伺服器已同意進行通信，但尚未進行HTTP通信。 這種延遲類型取決於客戶端和伺服器之間的基礎架構。 此過程要求在客戶機和伺服器之間找到通過Internet的路徑，並確保路由上的所有設備（如路由器和防火牆）都與資料傳輸相一致。
* 在透過TCP/IP連線傳送區段或資訊清單的HTTP要求時。

   伺服器會接收請求、處理請求，並開始將資料傳回用戶端。 延遲的程度取決於伺服器上軟體的負載和複雜性，而在客戶端發送請求時上載連接速度。

