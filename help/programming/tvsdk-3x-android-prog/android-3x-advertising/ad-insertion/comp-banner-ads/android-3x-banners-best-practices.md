---
title: 伴隨橫幅廣告的最佳做法
description: 伴隨橫幅廣告的最佳做法
copied-description: true
exl-id: e7d15916-9059-4993-a588-baf7d7ddc534
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 伴隨橫幅廣告的最佳做法 {#best-practices-for-companion-banner-ads}

TVSDK支援伴生條幅廣告，這些廣告是線性廣告的附帶廣告，線上性廣告結束後，通常會留在頁面上。 您的應用程式負責顯示隨線性廣告提供的伴隨橫幅。

顯示伴侶廣告時，請遵循以下建議：

* 嘗試在播放器佈局中顯示視頻廣告的夥伴橫幅廣告的數量。
* 僅當您的位置與廣告的指定高度和寬度匹配時，才顯示伴隨標題。

   >[!IMPORTANT]
   >
   >不要調整廣告的大小。

* 廣告開始後，請盡快開始呈現伴隨橫幅。
* 不要將主廣告/視頻容器與伴隨橫幅覆蓋。
* 廣告結束後，您可以顯示伴隨橫幅。

標準做法是顯示每個伴隨橫幅，直到您更換了廣告。
