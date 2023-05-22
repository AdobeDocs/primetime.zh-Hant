---
description: 對於啟用了回退規則的數字視頻廣告服務模板(VAST)廣告（或創意）,TVSDK將無效媒體類型的廣告視為空廣告，並嘗試在其位置使用回退廣告。 您可以配置回退行為的某些方面。
title: VAST和VMAP廣告的廣告回退
exl-id: 6575c08f-3a6a-4de5-b333-bceabbe00460
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# VAST和VMAP廣告的廣告回退 {#ad-fallback-for-vast-and-vmap-ads}

對於啟用了回退規則的數字視頻廣告服務模板(VAST)廣告（或創意）,TVSDK將無效媒體類型的廣告視為空廣告，並嘗試在其位置使用回退廣告。 您可以配置回退行為的某些方面。

VAST/數字視頻多廣告播放清單(VMAP)規範規定，對於啟用了VAST回退的廣告，空廣告會自動觸發回退廣告的使用。 當VAST廣告為空時，TVSDK在回退廣告中尋找有效的HLS媒體類型替換。 包裝中的VAST廣告具有無效的媒體類型時，TVSDK將此廣告視為空。 您可以配置TVSDK是否應對VMAP中內聯的廣告執行相同操作。 有關VAST的詳細資訊 `fallbackOnNoAd` 功能，請參閱 [數字視頻廣告服務模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

## 定義VMAP內聯廣告的回退廣告行為 {#define-fallback-ad-behavior-for-vmap-inline-ads}

當VMAP內聯廣告包含無效的媒體類型時，可以啟用回退。

1. 設定 `fallbackOnInvalidCreative` 如果HLS的線性/內聯ad的媒體類型無效，則VMAP將回退。

   預設值為false。 如果線性廣告因為其介質類型無效或無法重新打包廣告而失敗，則此標誌允許Migna時廣告決策遵循與廣告是空的VAST包裝相同的回退行為。

   ```
   var auditudeMetadata:AuditudeSettings = new AuditudeSettings(); 
   auditudeMetadata.fallbackOnInvalidCreative = true;
   ```

## VAST和VMAP的廣告回退行為 {#ad-fallback-behavior-for-vast-and-vmap}

當黃金時段廣告決策遇到空或媒體類型對HLS無效的VAST廣告（創意廣告）時，它會評估回退廣告以確定返回的內容。

<!--<a id="section_9F60AF00CE9645848EAAF8C06A9E426B"></a>-->

在TVSDK中，唯一有效的媒體類型是 `application/x-shockwave-flash` (VPAID)和 `application/x-mpegURL` (m3u8)。

當有獨立的回退廣告時，黃金時段廣告決策插件將按以下順序檢查這些廣告並返回第一個具有有效媒體類型的廣告：

1. 如果啟用重新打包，則第一次出現具有無效媒體類型的廣告時，會像處理其他無效媒體類型一樣處理。

   如果重新打包失敗，此過程將應用於廣告的其他事件。
1. 如果TVSDK找不到有效的回退廣告，則返回媒體類型無效的原始廣告。
1. 如果返回具有有效MIME類型的回退廣告而不是原始廣告，則Mighare廣告決策會將錯誤代碼403發送到VAST錯誤URL（如果可用）。
1. 如果回退廣告是包裝，並返回多個廣告，則只返回具有正確媒體類型的廣告。

>[!IMPORTANT]
>
>此行為始終為VAST包裝中的廣告啟用。 對於VMAP內聯的VAST廣告，預設情況下會禁用該行為，但您的應用程式可以啟用它。
