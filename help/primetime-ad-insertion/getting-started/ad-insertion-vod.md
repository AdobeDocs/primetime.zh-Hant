---
title: 使用Ad Insertion進行VOD
description: 使用VOD的Ad Insertion
exl-id: c998938e-f8a6-4ad3-97f6-ca4ad5055f15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 使用Ad Insertion進行VOD {#ad-insertion-vod}

PrimetimeAd Insertion支援使用標準VAST 3.0+或VMAP 1.0+格式將廣告插入多個VOD資產。

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD （廣告地圖） {#server-mapped-ads}

PrimetimeAd Insertion支援使用VMAP格式中定義的廣告時間表資訊，在開始播放之前插入廣告，以插入VOD插入。  VMAP專屬廣告追蹤（例如breakStart/breakEnd信標）將透過以下方式傳送： [廣告追蹤](set-up-ad-tracking.md).

## 完整事件重播(具有Ad Decisioning提示的VOD) {#full-event-replay}

PrimetimeAd Insertion也支援在內容串流本身包含提示的特殊VOD資產，例如可在先前錄製的即時事件播放中找到。 如需我們支援的廣告決策提示（或提示格式）型別的詳細資訊，請參閱 [在即時/線性中使用Ad Insertion](ad-insertion-live-linear-stream.md).

對於包含多個廣告插播的VOD資產，我們支援單一廣告請求和平行多個廣告請求情境。 如需詳細資訊，請參閱 `ptmulticall` 中的引數 [引數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). 串流提示支援VAST和VMAP格式。
