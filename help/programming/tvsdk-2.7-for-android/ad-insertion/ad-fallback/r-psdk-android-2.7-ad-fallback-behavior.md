---
description: 當Primetime廣告決策遇到空白或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估備援廣告以判斷要傳回的內容。
title: VAST和VMAP的廣告備援行為
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# VAST和VMAP {#ad-fallback-behavior-for-vast-and-vmap}的廣告備援行為

當Primetime廣告決策遇到空白或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估備援廣告以判斷要傳回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體類型是`application/x-mpegURL`(M3U8)。

當有獨立的後援廣告時，Primetime廣告決策外掛程式會依下列順序檢查這些廣告，並傳回第一個具有有效媒體類型的廣告：

1. 如果啟用重新封裝，則首次出現具有無效媒體類型的廣告會被視為其他無效媒體類型。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的備援廣告，則會傳回具有無效媒體類型的原始廣告。
1. 如果傳回具有有效MIME類型的備援廣告而非原始廣告，Primetime廣告決策會將錯誤碼403傳回至VAST錯誤URL（如果有的話）。
1. 如果備援廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體類型的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP內嵌的VAST廣告，行為預設會停用，但您的應用程式可以啟用它。

