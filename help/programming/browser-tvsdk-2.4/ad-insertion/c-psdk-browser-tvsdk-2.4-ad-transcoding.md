---
description: 部分協力廠商廣告（或創意）無法拼接至HTTP即時資料流(HLS)/HTTP動態自我調整資料流(DASH)內容資料流，因為其視訊格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可選擇嘗試將不相容的視訊重新封裝（轉碼）為相容的m3u8/mpd視訊。
title: 重新封裝（轉碼）不相容的廣告
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 重新封裝（轉碼）不相容的廣告{#repackage-transcode-incompatible-ads}

部分協力廠商廣告（或創意）無法拼接至HTTP即時資料流(HLS)/HTTP動態自我調整資料流(DASH)內容資料流，因為其視訊格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可選擇嘗試將不相容的視訊重新封裝（轉碼）為相容的m3u8/mpd視訊。

代理廣告伺服器、詳細目錄合作夥伴或廣告網路等各種協力廠商提供的廣告，通常會以不相容的格式傳送，例如漸進式下載MP4。
