---
description: 視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。
title: VPAID 2.0廣告支援
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# VPAID 2.0廣告支援{#vpaid-ad-support}

視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。

支援下列功能：

* VPAID規格2.0版

   如需詳細資訊，請參閱[IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 隨選視訊(VOD)內容上的線性VPAID廣告
* JavaScript VPAID廣告

   VPAID廣告必須以JavaScript為基礎，而廣告回應必須將VPAID廣告的媒體類型識別為`application/javascript`。

不支援下列功能：

* VPAID規格的1.0版
* 可跳過的廣告
* 非線性廣告，例如覆蓋廣告、動態伴侶廣告、可最小化廣告、可收合廣告和可展開廣告
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告

## API變更{#section_D62F3E059C6C493592D34534B0BFC150}

對API進行了下列變更：

* `getCustomAdView`函式已新增至`MediaPlayer`，並傳回轉譯VPAID廣告的Web檢視。

   如需此函式傳回之`CustomAdView`物件的詳細資訊，請參閱[API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html)。

* 從媒體播放器例項傳送`CUSTOM_AD`事件。

   應用程式可透過實作`CustomAdEventListener`來註冊事件回呼。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 可讓您變更VPAID載入程式的預設逾時。

   預設逾時值為10秒。

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

在播放VPAID廣告時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴使用者點選播放器檢視的程式碼無法運作。
* 主內容播放器會暫停，而播放器例項上對`pause`和`play`的呼叫則用來暫停和繼續VPAID廣告。

* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式的。

   廣告伺服器回應所定義的廣告持續時間和廣告分段總持續時間可能不正確。

## 實作VPAID 2.0整合{#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。

若要新增VPAID 2.0支援：

1. 將自訂廣告檢視新增至播放器介面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 新增自訂廣告事件的監聽器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
