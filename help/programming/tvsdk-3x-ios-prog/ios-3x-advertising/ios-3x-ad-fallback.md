---
description: 針對已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。
title: VAST和VMAP廣告的廣告遞補
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# VAST和VMAP廣告的廣告遞補 {#ad-fallback-for-vast-and-vmap-ads}

針對已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

VAST/Digital Video Multiple Ad Playlist (VMAP)規格指出，對於啟用VAST遞補的廣告，空白廣告會自動觸發遞補廣告的使用。 當VAST廣告為空白時，TVSDK會在遞補廣告中尋找有效的HLS媒體型別替代專案。 當包裝函式中的VAST廣告具有無效的媒體型別時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應該針對VMAP中的內嵌廣告執行相同動作。 如需VAST的詳細資訊 `fallbackOnNoAd` 功能，請參閱 [數位視訊廣告服務範本(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

## 定義VMAP內嵌廣告的遞補廣告行為 {#section_D90BB3C6E539472EABF000C0F616DBE2}

當VMAP內嵌廣告包含無效的媒體型別時，您可以開啟遞補。

1. 設定 `FallbackOnInvalidCreativeEnabled` 至 `YES` 線性內嵌廣告的媒體型別對HLS無效時，讓VMAP後援。

   >[!NOTE]
   >
   >預設值為NO。 如果線性廣告因媒體型別無效或無法重新封裝而失敗，此標幟可讓Primetime廣告決定遵循相同的遞補行為，就像廣告是空的VAST包裝函式一樣。

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## VAST和VMAP的廣告遞補行為 {#section_5B6716CC49CC4C40964CFE9F122C57A6}

當Primetime廣告決定遇到VAST廣告空白，或媒體型別對HLS無效時，它會評估遞補廣告以決定要傳回的內容。

在TVSDK中，唯一有效的媒體型別為 `application/x-mpegURL` (M3U8)。

如果有獨立的遞補廣告，Primetime ad Decisioning外掛程式會依照下列順序檢查這些廣告，並傳回第一個具有有效媒體型別的廣告：

1. 如果啟用重新封裝，系統會將第一次出現的無效媒體型別廣告視為其他無效媒體型別。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的遞補廣告，則會傳回媒體型別無效的原始廣告。
1. 如果傳回的是具有有效MIME型別的遞補廣告，而非原始廣告，Primetime廣告決定會將錯誤代碼403傳送至VAST錯誤URL （如果可用）。
1. 如果遞補廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體型別的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP中內嵌的VAST廣告，預設會停用行為，但您的應用程式可以啟用它。
