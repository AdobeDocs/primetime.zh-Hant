---
description: TVSDK支援在廣告插播時顯示線性視訊播放器——廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版也可與Browser TVSDK和JavaScript搭配使用。
seo-description: TVSDK支援在廣告插播時顯示線性視訊播放器——廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版也可與Browser TVSDK和JavaScript搭配使用。
seo-title: 在廣告插播中顯示線性VPAID廣告
title: 在廣告插播中顯示線性VPAID廣告
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 在廣告插播中顯示線性VPAID廣告{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK支援在廣告插播時顯示線性視訊播放器——廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版也可與Browser TVSDK和JavaScript搭配使用。

若要正確顯示VPAID廣告，您必須在例項中提供廣 `AdContainerView`告容器( `MediaPlayerContext` )。

VPAID廣告的限制：

* VPAID廣告不一定有預先定義的持續時間，因為廣告可以是互動式的。 因此，廣告持續時間（由廣告伺服器回應定義）不一定完全對應於廣告的真實持續時間。
* 對於VPAID 1.0廣告，TVSDK需要在裝置上安裝Flash Player 14.0.0.160或更新版本。 對於舊版Flash Player，此功能已停用，而且會略過VPAID 1.0廣告。

若要設定廣告容器，以便在廣告分隔內顯示VPAID廣告（1.0或2.0版）:

1. 使用下列范常式式碼來設定可顯示VPAID廣告的廣告容器。

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. 當檢視重新調整大小時，請重設廣告容器的大小。

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >當您取得全螢幕變更事件並在廣告容器上設定新大小時，請依照下列方式傳遞舞台顯示狀態，以確保播放器可正確調整大小：
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

