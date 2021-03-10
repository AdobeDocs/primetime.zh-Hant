---
description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
title: 廣泛廣告和VMAP廣告的廣告後援
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# 廣泛廣告和VMAP廣告的廣告後援{#ad-fallback-for-vast-and-vmap-ads}

對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。

VAST/Digital Video Multiple Ad Playlist(VMAP)規格指出，對於啟用VAST備援的廣告，空白廣告會自動觸發備援廣告的使用。 當VAST廣告為空時，TVSDK會在備援廣告中尋找有效的HLS媒體類型取代。 當包裝函式中的VAST廣告具有無效的媒體類型時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應針對VMAP內嵌的廣告執行相同動作。 有關VAST `fallbackOnNoAd`功能的詳細資訊，請參閱[數字視頻廣告服務模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

## 定義VMAP內嵌廣告的備援廣告行為{#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內嵌廣告包含無效的媒體類型時，您可以開啟備援。

1. 將`fallbackOnInvalidCreative`設為true，當線性／內嵌廣告的媒體類型對HLS無效時，VMAP會回落。

   預設值為false。 如果線性廣告因為媒體類型無效或廣告無法重新封裝而失敗，此標幟可讓Primetime廣告決策遵循與廣告為空的VAST包裝函式相同的備援行為。

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## VAST和VMAP {#ad-fallback-behavior-for-vast-and-vmap}的廣告備援行為

當Primetime廣告決策遇到空白或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估備援廣告以判斷要傳回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體類型是`application/x-shockwave-flash`(VPAID)和`application/x-mpegURL`(m3u8)。

當有獨立的後援廣告時，Primetime廣告決策外掛程式會依下列順序檢查這些廣告，並傳回具有有效媒體類型的第一個廣告：

1. 如果啟用重新封裝，則首次出現具有無效媒體類型的廣告會被視為其他無效媒體類型。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的備援廣告，則會傳回具有無效媒體類型的原始廣告。
1. 如果傳回具有有效MIME類型的備援廣告，而非原始廣告，Primetime廣告決策會將錯誤碼403傳送至VAST錯誤URL（如果有的話）。
1. 如果備援廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體類型的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP內嵌的VAST廣告，行為預設會停用，但您的應用程式可以啟用它。