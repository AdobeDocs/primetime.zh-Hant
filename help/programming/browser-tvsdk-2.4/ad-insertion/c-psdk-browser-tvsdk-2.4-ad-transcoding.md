---
description: 某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)/HTTP(DASH)動態自適應流(DASH)內容流中，因為其視頻格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可以選擇嘗試將不相容的視頻重新打包（轉碼）到相容的m3u8/mpd視頻中。
title: 重新打包（轉碼）不相容的廣告
exl-id: aaa78d5a-4b4b-4d50-b516-d39b47174487
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 重新打包（轉碼）不相容的廣告{#repackage-transcode-incompatible-ads}

某些第三方廣告（或創意）無法縫合到HTTP即時流(HLS)/HTTP(DASH)動態自適應流(DASH)內容流中，因為其視頻格式與HLS/DASH不相容。 Adobe Primetime廣告插入和瀏覽器TVSDK可以選擇嘗試將不相容的視頻重新打包（轉碼）到相容的m3u8/mpd視頻中。

來自不同第三方（如代理廣告伺服器、您的清單合作夥伴或廣告網路）的廣告通常以不相容的格式提供，如累進下載MP4。
