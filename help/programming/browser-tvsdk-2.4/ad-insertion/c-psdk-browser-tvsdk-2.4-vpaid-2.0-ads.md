---
description: 視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。
seo-description: 視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。
seo-title: VPAID 2.0廣告支援
title: VPAID 2.0廣告支援
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VPAID 2.0廣告支援 {#vpaid-ad-support}

視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。

支援下列功能：

* VPAID規格2.0版

   如需詳細資訊，請 [參閱IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/)。
* 具有隨選視訊(VOD)內容的線性VPAID廣告
* 在即時內容中，瀏覽器TVSDK支援前置JavaScript VPAID廣告。
* 在Flash備援模式中，瀏覽器TVSDK僅支援Flash型VPAID廣告。
* 線性JavaScript VPAID廣告

   VPAID廣告必須以JavaScript為基礎，而廣告回應必須將VPAID廣告的媒體類型識別為 `application/javascript`。

不支援下列功能：

* VPAID規格的1.0版
* 可跳過的廣告
* 非線性廣告，例如覆蓋廣告、動態伴侶廣告、可最小化廣告、可收合廣告和可展開廣告。
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* Flash VPAID廣告

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

下列API元素支援VPAID 2.0廣告：

* 此方 `getCustomAdView` 法傳 `MediaPlayer` 回物 `CustomAdView` 件，其代表轉譯VPAID廣告的Web檢視。

   如需方法的詳細資 `getCustomAdView` 訊，請參 [閱MediaPlayer API檔案](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 設定VPAID載入程式的逾時。

   預設逾時值為10秒。

* API可讓 `auditudeSettings.ignoreVPAIDAds`您忽略從Auditude伺服器收到的VPAID廣告。 API不適用於Flash備援。

在播放VPAID廣告時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴使用者點選播放器檢視的程式碼無法運作。
* 在播放器例項上暫停和播放的呼叫會暫停並繼續VPAID廣告。
* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式的。

   廣告伺服器回應中指定的廣告持續時間和廣告分段持續時間總計可能不正確。