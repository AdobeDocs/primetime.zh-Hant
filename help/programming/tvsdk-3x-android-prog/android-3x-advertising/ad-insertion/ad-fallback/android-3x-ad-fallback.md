---
description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
keywords: zero length ad;empty ad
seo-description: 對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。
seo-title: 廣泛廣告和VMAP廣告的廣告後援
title: 廣泛廣告和VMAP廣告的廣告後援
uuid: 688f0b67-9f5b-4c21-ab33-86d21580fbe9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 廣泛廣告和VMAP廣告的廣告後援 {#ad-fallback-for-vast-and-vmap-ads}

對於啟用後援規則的數位視訊廣告服務範本(VAST)廣告（或創意素材）,TVSDK會將無效媒體類型的廣告視為空白廣告，並嘗試在其位置使用後援廣告。 您可以設定備援行為的某些方面。

VAST/Digital Video Multiple Ad Playlist(VMAP)規格指出，對於啟用VAST備援的廣告，空白廣告會自動觸發備援廣告的使用。 當VAST廣告為空時，TVSDK會在備援廣告中尋找有效的HLS媒體類型取代。 當包裝函式中的VAST廣告具有無效的媒體類型時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應針對VMAP內嵌的廣告執行相同動作。 如需VAST功能的詳細資 `fallbackOnNoAd` 訊，請參 [閱數位視訊廣告服務範本(VAST)3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast)。

>[!NOTE]
>
>**零長度廣告** -當TVSDK遇到包含零持續時間廣告的廣泛回應，或沒有廣告的廣告插播時，會針對這些零長度廣告插播觸發AD_BREAK_START / AD_BREAK_COMPLETE事件。 *此行為僅適用於VOD串流。* 即使您的應用程式使用SKIP廣告政策，TVSDK仍會觸發這些事件。
>
>TVSDK不 *會針對即時串流* ，或當使用者運用特技播放或尋求超過零長廣告時，觸發AD_BREAK_START / AD_BREAK_COMPLETE事件。