---
description: TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。
seo-description: TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。
seo-title: 可點選廣告
title: 可點選廣告
uuid: 8b257483-8b90-47cf-be2a-095b6d5b8883
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 可點選廣告 {#clickable-ads}

TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。

在iOS適用的TVSDK中，只有線性廣告可點選。

## 回應廣告的點按次數 {#section_537AF2593FDB4257B81AAE2103B0C719}

當使用者點按廣告、配套橫幅廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供您點按之目標URL的相關資訊。

1. 若要設定TVSDK的事件偵聽器，並提供點進資訊，請新增觀察器 `PTMediaPlayerAdClickNotification`。

   >[!NOTE]
   >
   >當使用者點按廣告、配套橫幅廣告或相關按鈕時，TVSDK會派單此通知，包括點按目的地的相關資訊。

1. 在可點選廣告上監控使用者互動。
1. 當使用者觸碰或按一下廣告或按鈕時，若要通知TVSDK，請使用 `[_player notifyClick:_currentAd.primaryAsset];`。
1. 聽取TVSDK `PTMediaPlayerAdClickNotification` 的活動。
1. 若要擷取點進URL和相關資訊，請使用物 `PTMediaPlayerAdClickURLKey` 件。
1. 暫停影片。
1. 使用點進資訊來顯示廣告點進URL及相關資訊。

   >[!NOTE]
   >
   >例如，您可以以下列其中一種方式顯示資訊：

   * 在您的應用程式中，在瀏覽器中開啟點進URL。

      在案頭平台上，視訊廣告播放區域用於在使用者點按時叫用點進URL。
   * 將使用者重新導向至其外部行動網頁瀏覽器。

      在行動裝置上，視訊廣告播放區域用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全螢幕等。 在這些裝置上，會使用個別的檢視（例如贊助者按鈕）來啟動點進URL。

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
