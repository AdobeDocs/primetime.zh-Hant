---
title: 使用Ad Insertion進行視頻點播
description: 使用Ad Insertion進行視頻點播
exl-id: c998938e-f8a6-4ad3-97f6-ca4ad5055f15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 使用Ad Insertion進行視頻點播 {#ad-insertion-vod}

黃金時段Ad Insertion支援使用標準VAST 3.0+或VMAP 1.0+格式將廣告插入多個VOD資產。

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB宏](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD（廣告地圖） {#server-mapped-ads}

黃金時段Ad Insertion支援VOD插入，在使用以VMAP格式定義的廣告時間線資訊開始播放之前插入廣告。  VMAP特定廣告跟蹤（如breakStart/breakEnd信標）將隨 [廣告跟蹤](set-up-ad-tracking.md)。

## 完全事件重播(帶Ad Decisioning提示的VOD) {#full-event-replay}

黃金時段Ad Insertion還支援包含內容流本身中的提示的專用VOD資產，例如在先前錄制的實況事件的回放中發現的。 有關我們支援的廣告決策提示（或提示格式）類型的詳細資訊，請參見 [在即時/線性中使用Ad Insertion](ad-insertion-live-linear-stream.md)。

對於包含多個廣告片段的視頻點播資產，我們支援單個廣告請求和並行多個廣告請求場景。 有關詳細資訊，請參見 `ptmulticall` 參數 [參數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)。 支援VAST和VMAP格式用於流內提示。
