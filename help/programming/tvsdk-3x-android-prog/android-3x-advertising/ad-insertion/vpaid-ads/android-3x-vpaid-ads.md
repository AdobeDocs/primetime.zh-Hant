---
description: 視訊播放器廣告服務介面定義(VPAID) 2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更精確地鎖定廣告、追蹤廣告印象並從視訊內容獲利。
title: VPAID 2.0廣告支援
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 概觀 {#vpaid-ad-support-overview}

視訊播放器廣告服務介面定義(VPAID) 2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更精確地鎖定廣告、追蹤廣告印象並從視訊內容獲利。

支援下列功能：

* VPAID規格的2.0版

  如需詳細資訊，請參閱 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* 線性VPAID廣告搭配隨選影片(VOD)內容
* JavaScript VPAID廣告

  VPAID廣告必須以JavaScript為基礎，且廣告回應必須將VPAID廣告的媒體型別識別為 `application/javascript`.

不支援下列功能：

* VPAID規格的1.0版
* 可略過的廣告
* 非線性廣告，例如覆蓋廣告、動態隨附廣告、可最小化廣告、可摺疊廣告和可展開廣告
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告

## API

下列API元素支援VPAID 2.0廣告：

* 此 `getCustomAdView` 方法 `MediaPlayer` 傳回 `CustomAdView` 物件，代表轉譯VPAID廣告的Web檢視(請參閱 [API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html))。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 設定VPAID載入程式的逾時。 預設逾時值為10秒。

當VPAID廣告播放時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴播放器檢視上使用者點選的程式碼無法運作。
* 呼叫目標 `pause` 和 `play` 在播放器例項上暫停並繼續VPAID廣告。

* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式。

  在廣告伺服器回應中指定的廣告持續時間和廣告插播總持續時間可能不準確。
