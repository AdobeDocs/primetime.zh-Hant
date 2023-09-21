---
description: 部分協力廠商廣告（或創意）無法拼接至HTTP即時資料流(HLS)/透過HTTP (DASH)內容資料流的動態自我調整資料流，因為其視訊格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可選擇嘗試將不相容的視訊重新封裝（轉碼）為相容的m3u8/mpd視訊。
title: 重新封裝（轉碼）不相容的廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 重新封裝（轉碼）不相容的廣告{#repackage-transcode-incompatible-ads}

部分協力廠商廣告（或創意）無法拼接至HTTP即時資料流(HLS)/透過HTTP (DASH)內容資料流的動態自我調整資料流，因為其視訊格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可選擇嘗試將不相容的視訊重新封裝（轉碼）為相容的m3u8/mpd視訊。

由不同協力廠商提供的廣告，例如代理商廣告伺服器、您的詳細目錄合作夥伴或廣告網路，通常會以不相容的格式傳送，例如漸進式下載MP4。
