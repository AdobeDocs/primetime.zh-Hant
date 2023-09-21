---
description: 針對已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。
keywords: 零長度廣告；空白廣告
title: VAST和VMAP廣告的廣告遞補
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# VAST和VMAP廣告的廣告遞補 {#ad-fallback-for-vast-and-vmap-ads}

針對已啟用遞補規則的數位視訊廣告服務範本(VAST)廣告（或創意），TVSDK會將具有無效媒體型別的廣告視為空白廣告，並嘗試在其位置使用遞補廣告。 您可以設定遞補行為的某些方面。

VAST/Digital Video Multiple Ad Playlist (VMAP)規格指出，對於已啟用VAST遞補功能的廣告，空白廣告會自動觸發遞補廣告的使用。 當VAST廣告為空白時，TVSDK會在遞補廣告中尋找有效的HLS媒體型別替代專案。 當包裝函式中的VAST廣告具有無效的媒體型別時，TVSDK會將此廣告視為空白。 您可以設定TVSDK是否應該針對VMAP中的內嵌廣告執行相同動作。 如需VAST的詳細資訊 `fallbackOnNoAd` 功能，請參閱 [數位視訊廣告服務範本(VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**長度為零的廣告**  — 當TVSDK遇到VAST回應包含零持續時間廣告，或廣告插播不含廣告時，它會針對這些零長度廣告插播引發AD_BREAK_START / AD_BREAK_COMPLETE事件。 *此行為僅適用於VOD資料流。* 即使您的應用程式使用SKIP廣告原則，TVSDK也會觸發這些事件。
>
>TVSDK會 *非* 引發即時資料流的AD_BREAK_START / AD_BREAK_COMPLETE事件，或是當使用者採用Trickplay或Seek越過零長度廣告時。
