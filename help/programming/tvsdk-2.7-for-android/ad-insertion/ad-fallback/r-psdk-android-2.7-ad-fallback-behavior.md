---
description: 當Primetime ad decisioningencounters為空白或媒體型別對HLS無效的VAST廣告（創意）時，會評估遞補廣告以決定要傳回的內容。
title: VAST和VMAP的廣告遞補行為
exl-id: 8145d928-5d38-40f1-8dc3-fee9b815465c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# VAST和VMAP的廣告遞補行為 {#ad-fallback-behavior-for-vast-and-vmap}

當Primetime ad decisioningencounters為空白或媒體型別對HLS無效的VAST廣告（創意）時，會評估遞補廣告以決定要傳回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體型別為 `application/x-mpegURL` (M3U8)。

如果有獨立的遞補廣告，Primetime ad decisioningplug-in會依照下列順序檢查這些廣告，並傳回第一個具有有效媒體型別的廣告：

1. 如果啟用重新封裝，系統會將第一次出現的無效媒體型別廣告視為其他無效媒體型別。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的遞補廣告，則會傳回媒體型別無效的原始廣告。
1. 如果傳回的是具有有效MIME型別的遞補廣告，而不是原始廣告，Primetime ad decisionings會將錯誤代碼403傳送至VAST錯誤URL （如果可用）。
1. 如果遞補廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體型別的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP中內嵌的VAST廣告，行為預設為停用，但您的應用程式可以啟用它。
