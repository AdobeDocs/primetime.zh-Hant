---
title: 快取
description: 快取
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# HTTP快取{#caching}

PrimetimeAd Insertion預設會在擷取廣告創作元素和內容時遵循HTTP快取控制標題。  這可大幅降低PrimetimeAd Insertion在所有用戶端上對CDN進行網路要求的數量。  對於快取，Adobe建議進行下列設定，並涉及從CDN傳送HTTP標題`max-age`。  請連絡您的CDN代表，以在視訊串流和廣告串流上啟用這些標題。

## 針對即時／線性內容{#caching-live-linear-content}

* 主資訊清單：24小時，或快取控制：max-age=86400
* 媒體資訊清單：1秒，或快取控制：max-age=1

## 針對VOD內容{#caching-vod-content}

* 主資訊清單：24小時，或快取控制：max-age=86400
* 媒體資訊清單：24小時，或快取控制：max-age=86400
