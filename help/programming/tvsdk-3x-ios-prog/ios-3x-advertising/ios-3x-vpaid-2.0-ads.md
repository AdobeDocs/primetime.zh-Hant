---
description: 視頻播放器廣告服務介面定義(VPAID)2.0提供了播放視頻廣告的通用介面。 它為用戶提供了豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告印象和將視頻內容貨幣化。
title: VPAID 2.0廣告支援
exl-id: 6d29e53c-8fb4-4dd7-9859-8c105923bdef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# VPAID 2.0廣告支援 {#vpaid-ad-support}

視頻播放器廣告服務介面定義(VPAID)2.0提供了播放視頻廣告的通用介面。 它為用戶提供了豐富的媒體體驗，使出版商能夠更好地定位廣告、跟蹤廣告印象和將視頻內容貨幣化。

支援以下功能：

* VPAID規範的2.0版

   有關詳細資訊，請參閱 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 視頻點播(VOD)內容上的線性VPAID廣告
* JavaScript VPAID廣告

   VPAID廣告必須基於JavaScript，廣告響應必須將VPAID廣告的媒體類型標識為 `application/javascript`。

不支援以下功能：

* VPAID規範的1.0版
* 可跳過的廣告
* 非線性廣告，如覆蓋廣告、動態伴侶廣告、最小化廣告、可折疊廣告和可擴展廣告
* 預載入VPAID廣告
* 即時內容中的VPAID廣告
* FlashVPAID廣告
* 後卷VPAID廣告

## API更改 {#section_D62F3E059C6C493592D34534B0BFC150}

對API進行了以下更改：

* `PTAuditudeMetadata` 有 `customAdLoadTimeout` 屬性，以更改VPAID載入進程上的預設超時。

   預設超時值為10秒。

* `PTMediaPlayerCustomAdNotification` 從 `PTMediaPlayer` 實例

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

在播放VPAID廣告時：

* VPAID廣告顯示在播放器視圖上方的視圖容器中，因此依賴於用戶在播放器視圖上的點擊的代碼不起作用。
* 主內容播放器已暫停，並調用 `pause` 和 `play` 在播放器實例上用於暫停和恢復VPAID廣告。

* VPAID廣告沒有預定義的持續時間，因為廣告可以是互動式的。

   由廣告伺服器響應定義的廣告持續時間和廣告中斷持續時間總數可能不準確。

## 實施VPAID 2.0整合 {#section_63C9C737367C4A0AB4D62E0DC2084141}

要在iOS應用程式中添加VPAID 2.0支援，請執行以下操作：

1. （可選）為自定義廣告事件添加偵聽器。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. （可選）顯示通知。

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```
