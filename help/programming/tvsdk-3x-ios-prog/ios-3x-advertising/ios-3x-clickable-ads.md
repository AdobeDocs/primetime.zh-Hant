---
description: TVSDK提供資訊，以便您能夠對點擊廣告進行操作。 在建立播放器UI時，必須決定當用戶按一下可按一下廣告時如何響應。
title: 可點擊的廣告
exl-id: 4c4d37ee-0353-4c0f-8a11-d9be9bd427ec
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 可點擊的廣告 {#clickable-ads}

TVSDK提供資訊，以便您能夠對點擊廣告進行操作。 在建立播放器UI時，必須決定當用戶按一下可按一下廣告時如何響應。

在iOS的TVSDK中，只有線性廣告可點擊。

## 響應廣告點擊 {#section_537AF2593FDB4257B81AAE2103B0C719}

當用戶按一下廣告、伴隨橫幅廣告或相關按鈕時，您的應用程式必須響應。 TVSDK提供有關按一下的目標URL的資訊。

1. 要為TVSDK設定事件偵聽器並提供點擊資訊，請為 `PTMediaPlayerAdClickNotification`。

   >[!NOTE]
   >
   >當用戶按一下廣告、夥伴橫幅廣告或相關按鈕時，TVSDK會調度此通知，包括有關按一下的目的地的資訊。

1. 監視可點擊廣告上的用戶交互。
1. 當用戶觸摸或按一下廣告或按鈕時，要通知TVSDK，請使用 `[_player notifyClick:_currentAd.primaryAsset];`。
1. 聽著 `PTMediaPlayerAdClickNotification` TVSDK中的事件。
1. 要檢索點擊式URL和相關資訊，請使用 `PTMediaPlayerAdClickURLKey` 的雙曲餘切值。
1. 暫停視頻。
1. 使用點擊資訊顯示廣告點擊URL和相關資訊。

   >[!NOTE]
   >
   >例如，可以通過以下方式之一顯示資訊：

   * 在應用程式中，在瀏覽器中開啟「點擊」URL。

      在案頭平台上，視頻和播放區域用於在用戶點擊時調用點擊式URL。
   * 將用戶重定向到其外部移動Web瀏覽器。

      在移動設備上，視頻和播放區域用於其他功能，如隱藏和顯示控制項、暫停播放、擴展到全屏等。 在這些設備上，使用單獨的視圖（如發起人按鈕）來啟動點擊式URL。

1. 關閉其中顯示點擊資訊的瀏覽器窗口並繼續播放視頻。

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
