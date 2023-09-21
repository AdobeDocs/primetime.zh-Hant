---
description: TVSDK會提供您資訊，方便您對點進廣告採取行動。 當您建立播放器UI時，必須決定當使用者點按可點按廣告時如何回應。
title: 可點按的廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 可點按的廣告{#clickable-ads}

TVSDK會提供您資訊，方便您對點進廣告採取行動。 當您建立播放器UI時，必須決定當使用者點按可點按廣告時如何回應。

在適用於iOS的TVSDK中，只有線性廣告可供點按。

## 回應廣告的點按 {#section_537AF2593FDB4257B81AAE2103B0C719}

當使用者點選廣告、隨附橫幅廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供點按的目的地URL相關資訊。

1. 若要設定TVSDK的事件監聽器，並提供點進資訊，請新增觀察者 `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >當使用者點按廣告、隨附橫幅廣告或相關按鈕時，TVSDK會傳送此通知，包括點按目的地的相關資訊。

1. 監視使用者在可點按廣告上的互動。
1. 當使用者觸控或點選廣告或按鈕要通知TVSDK，使用 `[_player notifyClick:_currentAd.primaryAsset];`.
1. 聆聽 `PTMediaPlayerAdClickNotification` TVSDK的事件。
1. 若要擷取點進URL和相關資訊，請使用 `PTMediaPlayerAdClickURLKey` 物件。
1. 暫停視訊。
1. 使用點進資訊來顯示廣告點進URL和相關資訊。

   >[!NOTE]
   >
   >例如，您可以用下列其中一種方式來顯示資訊：

   * 在您的應用程式中，在瀏覽器中開啟點進URL。

     在案頭平台上，視訊廣告播放區域是用來在使用者點按時叫用點進URL。
   * 將使用者重新導向至其外部行動網頁瀏覽器。

     在行動裝置上，視訊廣告播放區域可用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全熒幕等。 在這些裝置上，會使用個別檢視（例如贊助者按鈕）來啟動點進URL。

1. 關閉顯示點進資訊的瀏覽器視窗，然後繼續播放視訊。

   例如：

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
