---
description: 視頻播放器廣告服務介面定義(VPAID)2.0提供了播放視頻廣告的通用介面。 它為用戶提供了豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告印象和將視頻內容貨幣化。
title: VPAID 2.0廣告支援
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# VPAID 2.0廣告支援 {#vpaid-ad-support}

視頻播放器廣告服務介面定義(VPAID)2.0提供了播放視頻廣告的通用介面。 它為用戶提供了豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告印象和將視頻內容貨幣化。

支援以下功能：

* VPAID規範的2.0版

   有關詳細資訊，請參見 [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/)。
* 具有視頻點播(VOD)內容的線性VPAID廣告
* 在即時內容中，瀏覽器TVSDK支援預卷JavaScript VPAID廣告。
* 在Flash回退模式下，瀏覽器TVSDK僅支援基於Flash的VPAID廣告。
* 線性JavaScript VPAID廣告

   VPAID廣告必須基於JavaScript，廣告響應必須將VPAID廣告的媒體類型標識為 `application/javascript`。

不支援以下功能：

* VPAID規範的1.0版
* 可跳過的廣告
* 非線性廣告，如覆蓋廣告、動態伴侶廣告、可最小化廣告、可折疊廣告和可擴展廣告。
* 預載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

以下API元素支援VPAID 2.0廣告：

* 的 `getCustomAdView` 方法 `MediaPlayer` 返回 `CustomAdView` 對象，它表示呈現VPAID廣告的Web視圖。

   有關 `getCustomAdView` 方法，請參見 [MediaPlayer API文檔](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 設定VPAID載入進程的超時。

   預設超時值為10秒。

* API `auditudeSettings.ignoreVPAIDAds`，允許您忽略從Auditude伺服器接收的VPAID廣告。 API不適用於Flash回退。

在播放VPAID廣告時：

* VPAID廣告顯示在播放器視圖上方的視圖容器中，因此依賴於用戶在播放器視圖上的點擊的代碼不起作用。
* 呼叫暫停並播放播放器實例暫停並恢復VPAID廣告。
* VPAID廣告沒有預定義的持續時間，因為廣告可以是互動式的。

   在廣告伺服器響應中指定的廣告持續時間和廣告中斷持續時間總數可能不準確。
