---
title: 最佳化視訊啟動時間
description: 最佳化視訊啟動時間
exl-id: 5a89c774-0fed-4378-9cf8-98c4c843ae0d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 最佳化視訊啟動時間概觀 {#optimize-video-start-up-times}

PrimetimeAd Insertion提供數項功能來最佳化視訊啟動時間，例如快取和路由/通訊協定最佳化的規則。 以下是使用PrimetimeAd Insertion時為確保影片更快速啟動而建議的其他幾項內容：

* 從內容傳遞網路(CDN)提供所有廣告和內容

* 減少或移除PrimetimeAd Insertion和CDN之間的TLS握手。 如需詳細資訊，請參閱 [最佳化路由和通訊協定](optimize-routes-protocols.md).

* 從相同的CDN提供廣告和內容片段

* 為即時/VOD內容和資訊清單插入快取控制標頭

* 減少或移除回應緩慢的廣告提供者或廣告創意
