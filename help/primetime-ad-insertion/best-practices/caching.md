---
title: 快取
description: 快取
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP快取 {#caching}

擷取廣告創意與內容時，PrimetimeAd Insertion預設會遵循HTTP快取控制標頭。  這可大幅減少PrimetimeAd Insertion跨所有使用者端向CDN提出網路要求所需的數量。  對於快取，Adobe建議進行以下設定並涉及傳送HTTP標頭 `max-age` 從您的CDN.  請聯絡您的CDN代表，為您的視訊串流和廣告串流啟用這些標題。

## 適用於即時/線性內容 {#caching-live-linear-content}

* 主要資訊清單： 24小時，或Cache-Control： max-age=86400
* 媒體資訊清單： 1秒，或Cache-Control： max-age=1

## 針對VOD內容 {#caching-vod-content}

* 主要資訊清單： 24小時，或Cache-Control： max-age=86400
* 媒體資訊清單： 24小時，或Cache-Control： max-age=86400
