---
description: 當黃金時段廣告決策遇到空或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估回退廣告以確定返回的內容。
title: VAST和VMAP的廣告回退行為
exl-id: 65814b91-6528-4eea-abfb-f45dd2dbb899
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# VAST和VMAP的廣告回退行為 {#ad-fallback-behavior-for-vast-and-vmap}

當黃金時段廣告決策遇到空或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估回退廣告以確定返回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體類型是 `application/x-mpegURL` (M3U8)。

當有獨立的後備廣告時，黃金時段廣告決策插件會按以下順序檢查這些廣告，並返回第一個具有有效媒體類型的廣告：

1. 如果啟用重新打包，則第一次出現具有無效媒體類型的廣告時，會像處理其他無效媒體類型一樣處理。

   如果重新打包失敗，此過程將應用於廣告的其他事件。
1. 如果TVSDK找不到有效的回退廣告，則返回媒體類型無效的原始廣告。
1. 如果返回具有有效MIME類型的回退廣告而不是原始廣告，則Mighine廣告決策會將錯誤代碼403發送到VAST錯誤URL（如果可用）。
1. 如果回退廣告是包裝，並返回多個廣告，則只返回具有正確媒體類型的廣告。

>[!IMPORTANT]
>
>此行為始終為VAST包裝中的廣告啟用。 對於VMAP內聯的VAST廣告，預設情況下會禁用該行為，但您的應用程式可以啟用它。
