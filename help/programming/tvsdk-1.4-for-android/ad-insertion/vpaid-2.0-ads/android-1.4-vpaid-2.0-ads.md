---
description: 影片播放器廣告服務介面定義(VPAID) 2.0提供播放影片廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更好地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。
title: VPAID 2.0廣告支援
exl-id: ee3e0cd9-463e-4de9-a94f-292e968b6f08
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# VPAID 2.0廣告支援 {#vpaid-ad-support}

影片播放器廣告服務介面定義(VPAID) 2.0提供播放影片廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更好地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。

支援下列功能：

* VPAID規格的2.0版

   如需詳細資訊，請參閱 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* 線性VPAID隨選影片(VOD)內容廣告
* JavaScript VPAID廣告

   VPAID廣告必須以JavaScript為基礎，且廣告回應必須將VPAID廣告的媒體型別識別為 `application/javascript`.

不支援下列功能：

* VPAID規格的1.0版
* 可略過的廣告
* 非線性廣告，例如覆蓋廣告、動態隨附廣告、可最小化廣告、可摺疊廣告和可展開廣告
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告

## API變更 {#section_D62F3E059C6C493592D34534B0BFC150}

已對API進行下列變更：

* A `getCustomAdView` 函式已新增至 `MediaPlayer` 和會傳迴轉譯VPAID廣告的Web檢視。

   如需更多有關「 」的資訊， `CustomAdView` 此函式傳回的物件，請參閱 [API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` 事件是從媒體播放器例項中傳送。

   應用程式可藉由實作 `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 可讓您變更VPAID載入程式的預設逾時。

   預設逾時值為10秒。

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

當VPAID廣告播放時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴播放器檢視上使用者點選的程式碼無法運作。
* 主要內容播放器已暫停，並呼叫 `pause` 和 `play` 播放器例項上的用來暫停和繼續VPAID廣告。

* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式。

   由廣告伺服器回應定義的廣告持續時間和廣告插播總持續時間可能不準確。

## 實作VPAID 2.0整合 {#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的監聽器。

若要新增VPAID 2.0支援：

1. 將自訂廣告檢視新增至播放器介面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 新增自訂廣告事件的接聽程式。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
