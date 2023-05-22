---
description: 對於啟用了回退規則的數字視頻廣告服務模板(VAST)廣告（或創意）,TVSDK將無效媒體類型的廣告視為空廣告，並嘗試在其位置使用回退廣告。 您可以配置回退行為的某些方面。
keywords: 零長度ad；空ad
title: VAST和VMAP廣告的廣告回退
exl-id: 5cabb5f6-b895-48bc-9c9e-b22dd47539bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# VAST和VMAP廣告的廣告回退 {#ad-fallback-for-vast-and-vmap-ads}

對於啟用了回退規則的數字視頻廣告服務模板(VAST)廣告（或創意）,TVSDK將無效媒體類型的廣告視為空廣告，並嘗試在其位置使用回退廣告。 您可以配置回退行為的某些方面。

VAST/數字視頻多廣告播放清單(VMAP)規範規定，對於啟用了VAST回退的廣告，空廣告會自動觸發備用廣告的使用。 當VAST廣告為空時，TVSDK在回退廣告中尋找有效的HLS媒體類型替換。 包裝中的VAST廣告具有無效的媒體類型時，TVSDK將此廣告視為空。 您可以配置TVSDK是否應對VMAP中內聯的廣告執行相同操作。 有關VAST的詳細資訊 `fallbackOnNoAd` 功能，請參閱 [數字視頻廣告服務模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

>[!NOTE]
>
>**零長度廣告**  — 當TVSDK遇到包含零持續時間廣告的VAST響應或沒有廣告的廣告中斷時，它會為這些零長度廣告中斷觸發AD_BREAK_START / AD_BREAK_COMPLETE事件。 *此行為僅適用於VOD流。* TVSDK即使您的應用使用SKIP廣告策略也會觸發這些事件。
>
>TVSDK做到 *不* 為即時流觸發AD_BREAK_START / AD_BREAK_COMPLETE事件，或當用戶使用滴播或尋求超過零長度的ad時。
