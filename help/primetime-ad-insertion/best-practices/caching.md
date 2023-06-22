---
title: 快取
description: 快取
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# http快取 {#caching}

擷取廣告創意和內容時，PrimetimeAd Insertion預設會遵循HTTP快取控制標頭。  這可大幅減少PrimetimeAd Insertion跨所有使用者端向CDN發出的網路要求數量。  對於快取，Adobe會建議進行下列設定，並且需要傳送HTTP標頭 `max-age` 從您的CDN.  請聯絡您的CDN代表，在您的視訊串流和廣告串流上啟用這些標頭。

## 適用於即時/線性內容 {#caching-live-linear-content}

* 主要資訊清單：24小時，或Cache-Control： max-age=86400
* 媒體資訊清單： 1秒，或Cache-Control： max-age=1

## 針對VOD內容 {#caching-vod-content}

* 主要資訊清單：24小時，或Cache-Control： max-age=86400
* 媒體資訊清單： 24小時或Cache-Control： max-age=86400
