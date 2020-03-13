---
description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
seo-description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
seo-title: 廣泛廣告和VMAP廣告的廣告後援
title: 廣泛廣告和VMAP廣告的廣告後援
uuid: 290f0aeb-7314-4615-b477-24e65d5857ac
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 廣泛廣告和VMAP廣告的廣告後援 {#ad-fallback-for-vast-and-vmap-ads}

對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。

VAST/Digital Video Multiple Ad Playlist(VMAP)規格指出，對於啟用VAST備援的廣告，空白廣告會自動觸發備援廣告的使用。 當VAST廣告為空時，TVSDK會在備援廣告中尋找有效的HLS媒體類型取代。 當包裝函式中的VAST廣告具有無效的媒體類型時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應針對VMAP內嵌的廣告執行相同動作。 如需VAST功能的詳細資 `fallbackOnNoAd` 訊，請參 [閱數位視訊廣告服務範本(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

## 定義VMAP內嵌廣告的備援廣告行為 {#section_D90BB3C6E539472EABF000C0F616DBE2}

當VMAP內嵌廣告包含無效的媒體類型時，您可以開啟備援。

1. 當線 `FallbackOnInvalidCreativeEnabled` 性／內 `YES` 嵌廣告的媒體類型對HLS無效時，設定為VMAP回退。

   >[!NOTE]
   >
   >預設值為NO。 如果線性廣告因為媒體類型無效或廣告無法重新封裝而失敗，此標幟可讓Primetime廣告決策遵循與廣告為空的VAST包裝函式相同的備援行為。

   ```
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.isFallbackOnInvalidCreativeEnabled = YES;
   ```

## VAST和VMAP的廣告備援行為 {#section_5B6716CC49CC4C40964CFE9F122C57A6}

當Primetime廣告決策遇到空白或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估備援廣告以判斷要傳回的內容。

在TVSDK中，唯一有效的媒體類 `application/x-mpegURL` 型為(M3U8)。

當有獨立的後援廣告時，Primetime廣告決策外掛程式會依下列順序檢查這些廣告，並傳回具有有效媒體類型的第一個廣告：

1. 如果啟用重新封裝，則首次出現具有無效媒體類型的廣告會被視為其他無效媒體類型。

   如果重新封裝失敗，此程式會套用至廣告的其他發生次數。
1. 如果TVSDK找不到有效的備援廣告，則會傳回具有無效媒體類型的原始廣告。
1. 如果傳回具有有效MIME類型的備援廣告，而非原始廣告，Primetime廣告決策會將錯誤碼403傳送至VAST錯誤URL（如果有的話）。
1. 如果備援廣告是包裝函式，並傳回多個廣告，則只會傳回具有正確媒體類型的廣告。

>[!IMPORTANT]
>
>VAST包裝函式中的廣告一律會啟用此行為。 對於VMAP內嵌的VAST廣告，行為預設會停用，但您的應用程式可以啟用它。

