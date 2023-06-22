---
description: 對於已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。
title: VAST和VMAP廣告的廣告遞補
exl-id: 65ec8ed6-17d1-47e3-8c4c-578371263e6d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# VAST和VMAP廣告的廣告遞補 {#ad-fallback-for-vast-and-vmap-ads}

對於已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

VAST/數位視訊多重廣告播放清單(VMAP)規格指出，對於啟用VAST遞補的廣告，空白廣告會自動觸發使用遞補廣告。 當VAST廣告為空白時，TVSDK會在遞補廣告中尋找有效的HLS媒體型別替代專案。 當包裝函式中的VAST廣告具有無效的媒體型別時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應該針對VMAP中的內嵌廣告執行相同動作。 如需有關VAST的詳細資訊 `fallbackOnNoAd` 功能，請參閱 [數位視訊廣告服務範本(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## 定義VMAP內嵌廣告的遞補廣告行為 {#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內嵌廣告包含無效的媒體型別時，您可以開啟遞補功能。

1. 設定 `setFallbackOnInvalidCreativeEnabled` 至 `true` 線性廣告/內嵌廣告的媒體型別對HLS無效時，讓VMAP後援。

   預設值為false。 如果線性廣告因媒體型別無效或無法重新封裝而失敗，此標幟可讓Primetime廣告決策遵循相同的遞補行為，就像廣告是空的VAST包裝函式一樣。

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

## VAST和VMAP的廣告遞補行為 {#ad-fallback-behavior-for-vast-and-vmap}

當Primetime廣告決策遇到空白或媒體型別對HLS無效的VAST廣告（創意）時，它會評估遞補廣告以決定要傳回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體型別為 `application/x-mpegURL` (M3U8)。

當有獨立的遞補廣告時，Primetime ad decisioning外掛程式會依照以下順序檢查這些廣告，並傳回第一個具有有效媒體型別的廣告：

1. 如果啟用重新封裝，系統會將第一次出現的無效媒體型別廣告視為其他無效媒體型別。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的遞補廣告，則會傳回媒體型別無效的原始廣告。
1. 如果傳回具有有效MIME型別的遞補廣告，而不是原始廣告，Primetime廣告決定會將錯誤代碼403傳送到VAST錯誤URL （如果可用）。
1. 如果遞補廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體型別的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP中內嵌的VAST廣告，行為預設為停用，但您的應用程式可以啟用它。
