---
description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
keywords: 零長度廣告；空廣告
title: 廣泛廣告和VMAP廣告的廣告後援
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# 概述{#ad-fallback-for-vast-and-vmap-ads-overview}

對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。

VAST/Digital Video Multiple Ad Playlist(VMAP)規格指出，對於啟用VAST備援的廣告，空白廣告會自動觸發備援廣告的使用。 當VAST廣告為空時，TVSDK會在備援廣告中尋找有效的HLS媒體類型取代。 當包裝函式中的VAST廣告具有無效的媒體類型時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應針對VMAP內嵌的廣告執行相同動作。 有關VAST `fallbackOnNoAd`功能的詳細資訊，請參閱[數字視頻廣告服務模板(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

>[!NOTE]
>
>**零長度廣告** -當TVSDK遇到包含零持續時間廣告的廣泛回應，或沒有廣告的廣告插播時，會針對這些零長度廣告插播觸發AD_BREAK_START / AD_BREAK_COMPLETE事件。*此行為僅適用於VOD串流。* 即使您的應用程式使用SKIP廣告政策，TVSDK仍會觸發這些事件。
>
>TVSDK會針對即時串流&#x200B;*not*&#x200B;觸發AD_BREAK_START / AD_BREAK_COMPLETE事件，或當使用者使用滴答或尋求超過零長廣告時。

