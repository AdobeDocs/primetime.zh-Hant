---
title: 使用廣告插入VOD
description: 使用廣告插入VOD
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 使用VOD {#ad-insertion-vod}的廣告插入

Primetime廣告插入支援使用標準VAST 3.0+或VMAP 1.0+格式將廣告插入多個VOD資產。

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD（廣告地圖）{#server-mapped-ads}

Primetime廣告插入支援VOD插入，使用VMAP格式中定義的廣告時間表資訊，在播放開始前插入廣告。  VMAP特定廣告追蹤（例如breakStart/breakEnd信標）將隨[廣告追蹤](set-up-ad-tracking.md)一起傳送。

## 完整事件重播（含廣告決策提示的VOD）{#full-event-replay}

Primetime廣告插入也支援在內容串流本身包含提示的專用VOD資產，例如在播放先前錄制的即時事件時發現的提示。 如需我們支援的廣告決策提示（或提示格式）類型的詳細資訊，請參閱[在即時／線性中使用廣告插入](ad-insertion-live-linear-stream.md)。

我們支援包含多個廣告插播的VOD資產的單一廣告請求和平行多個廣告請求藍本。 如需詳細資訊，請參閱[參數說明](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md)中的`ptmulticall`參數。 串流內提示支援VAST和VMAP格式。
