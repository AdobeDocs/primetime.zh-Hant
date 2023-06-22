---
description: 影片播放器廣告服務介面定義(VPAID) 2.0提供播放影片廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更好地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。
title: VPAID 2.0廣告支援
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# VPAID 2.0廣告支援 {#vpaid-ad-support}

影片播放器廣告服務介面定義(VPAID) 2.0提供播放影片廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更好地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。

支援下列功能：

* VPAID規格的2.0版

   如需詳細資訊，請參閱 [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* 具有隨選影片(VOD)內容的線性VPAID廣告
* 在即時內容中，瀏覽器TVSDK支援前段JavaScript VPAID廣告。
* 在Flash遞補模式中，瀏覽器TVSDK僅支援Flash型VPAID廣告。
* 線性JavaScript VPAID廣告

   VPAID廣告必須以JavaScript為基礎，且廣告回應必須將VPAID廣告的媒體型別識別為 `application/javascript`.

不支援下列功能：

* VPAID規格的1.0版
* 可略過的廣告
* 非線性廣告，例如覆蓋廣告、動態隨附廣告、可最小化廣告、可摺疊廣告和可展開廣告。
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

下列API元素支援VPAID 2.0廣告：

* 此 `getCustomAdView` 方法 `MediaPlayer` 傳回 `CustomAdView` 物件，代表轉譯VPAID廣告的Web檢視。

   如需更多有關「 」的資訊， `getCustomAdView` 方法，請參閱 [MediaPlayer API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 設定VPAID載入程式的逾時。

   預設逾時值為10秒。

* API、 `auditudeSettings.ignoreVPAIDAds`，可讓您忽略從Auditude伺服器接收的VPAID廣告。 API無法用於Flash遞補。

當VPAID廣告播放時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴播放器檢視上使用者點選的程式碼無法運作。
* 在播放器例項暫停和播放以及繼續VPAID廣告的呼叫。
* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式。

   在廣告伺服器回應中指定的廣告持續時間和廣告插播總持續時間可能不準確。
