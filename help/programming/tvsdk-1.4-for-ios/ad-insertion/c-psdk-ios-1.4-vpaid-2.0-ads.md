---
description: 影片播放器廣告服務介面定義(VPAID) 2.0提供播放影片廣告的通用介面。 它為使用者提供豐富的媒體體驗，並允許發佈者更好地鎖定廣告、追蹤廣告印象，以及從視訊內容獲利。
title: VPAID 2.0廣告支援
exl-id: 404e7c91-27ab-4cbd-ba97-8fdd81a41a25
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '323'
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
* 後置式VPAID廣告

## API變更 {#section_D62F3E059C6C493592D34534B0BFC150}

已對API進行下列變更：

* `PTAuditudeMetadata` 具有 `customAdLoadTimeout` 屬性以變更VPAID載入程式的預設逾時。

   預設逾時值為10秒。

* `PTMediaPlayerCustomAdNotification` 是從 `PTMediaPlayer` 例項

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

當VPAID廣告播放時：

* VPAID廣告會顯示在播放器檢視上方的檢視容器中，因此依賴播放器檢視上使用者點選的程式碼無法運作。
* 主要內容播放器已暫停，並呼叫 `pause` 和 `play` 播放器例項上的用來暫停和繼續VPAID廣告。

* VPAID廣告沒有預先定義的持續時間，因為廣告可以是互動式。

   由廣告伺服器回應定義的廣告持續時間和廣告插播總持續時間可能不準確。

## 實作VPAID 2.0整合 {#section_63C9C737367C4A0AB4D62E0DC2084141}

若要在您的iOS應用程式中新增VPAID 2.0支援：

1. （選用）新增自訂廣告事件的接聽程式。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. （選用）顯示通知。

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```
