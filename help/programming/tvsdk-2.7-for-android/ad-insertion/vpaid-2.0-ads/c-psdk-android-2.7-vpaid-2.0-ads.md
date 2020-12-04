---
description: 視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。
seo-description: 視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。
seo-title: VPAID 2.0廣告支援
title: VPAID 2.0廣告支援
uuid: 6485e387-2a13-476f-a0fd-91c6e19fd385
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# VPAID 2.0廣告支援{#vpaid-ad-support}

視訊播放器廣告服務介面定義(VPAID)2.0提供播放視訊廣告的通用介面。 它為使用者提供豐富的媒體體驗，讓出版業者能夠更精準地鎖定廣告、追蹤廣告印象，並從視訊內容獲利。

支援下列功能：

* VPAID規格2.0版

   如需詳細資訊，請參閱[IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 具有隨選視訊(VOD)內容的線性VPAID廣告
* JavaScript VPAID廣告

   VPAID廣告必須以JavaScript為基礎，而廣告回應必須將VPAID廣告的媒體類型識別為`application/javascript`。

不支援下列功能：

* VPAID規格的1.0版
* 可跳過的廣告
* 非線性廣告，例如覆蓋廣告、動態伴侶廣告、可最小化廣告、可收合廣告和可展開廣告
* 預先載入VPAID廣告
* 即時內容中的VPAID廣告
* Flash VPAID廣告

## API

下列API元素支援VPAID 2.0廣告：

* `MediaPlayer`的`getCustomAdView`方法傳回`CustomAdView`物件，代表轉譯VPAID廣告的Web檢視（請參閱[API參考](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)）。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 設定VPAID載入程式的逾時。預設逾時值為10秒。

在播放VPAID廣告時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴使用者點選播放器檢視的程式碼無法運作。
* 在播放器例項上呼叫`pause`和`play`會暫停並繼續VPAID廣告。

* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式的。

   廣告伺服器回應中指定的廣告持續時間和廣告分段持續時間總計可能不正確。