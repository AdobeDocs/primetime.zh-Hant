---
title: 最佳化視訊啟動時間
description: 最佳化視訊啟動時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---

# 最佳化視訊啟動時間概觀 {#optimize-video-start-up-times}

PrimetimeAd Insertion提供數項功能來最佳化視訊啟動時間，例如快取和路由/通訊協定最佳化的規則。 以下是使用PrimetimeAd Insertion時為確保更短的視訊啟動時間而提出的其他建議：

* 從內容傳遞網路(CDN)提供所有廣告和內容

* 減少或移除PrimetimeAd Insertion和CDN之間的TLS交握。 如需詳細資訊，請參閱 [最佳化路由和通訊協定](optimize-routes-protocols.md).

* 從相同的CDN提供廣告和內容片段

* 為即時/VOD內容和資訊清單插入cache-control標題

* 減少或移除回應緩慢的廣告提供者或廣告創意
