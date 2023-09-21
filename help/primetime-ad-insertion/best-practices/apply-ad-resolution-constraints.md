---
title: 套用廣告解析度限制
description: 套用廣告解析度限制
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 套用廣告解析度限制 {#apply-ad-resolution-constraints}

在某些情況下，特定廣告提供者可能會延遲回應，進而導致視訊啟動時間增加。 PrimetimeAd Insertion支援廣告請求逾時和整個廣告解析階段，以限制這些緩慢廣告提供者的影響。  如果下游廣告提供者回應速度太慢，也可以插入遞補廣告。  如需詳細資訊，請參閱 [`ptadtimeout` Bootstrap API中的引數](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md).
