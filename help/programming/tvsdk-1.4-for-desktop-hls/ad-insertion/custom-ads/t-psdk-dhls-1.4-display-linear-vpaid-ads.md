---
description: TVSDK支援在廣告插播中顯示線性視訊播放器廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版也可搭配瀏覽器TVSDK和JavaScript運作。
title: 在廣告插播中顯示線性VPAID廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 在廣告插播中顯示線性VPAID廣告{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK支援在廣告插播中顯示線性視訊播放器廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版也可搭配瀏覽器TVSDK和JavaScript運作。

若要正確顯示VPAID廣告，您必須提供廣告容器( `AdContainerView`)中 `MediaPlayerContext` 執行個體。

VPAID廣告的限制：

* VPAID廣告不一定有預先定義的持續時間，因為廣告可以是互動式。 因此，廣告持續時間（由廣告伺服器回應定義）不一定完全符合廣告的真實持續時間。
* 若是VPAID 1.0廣告，TVSDK需要將Flash播放器14.0.0.160或更新版本安裝在裝置上。 若為舊版Flash播放器，此功能會停用，並略過VPAID 1.0廣告。

若要設定在廣告插播中顯示VPAID廣告（1.0或2.0版）的廣告容器：

1. 使用以下範常式式碼來設定可顯示VPAID廣告的廣告容器。

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

1. 當檢視調整大小時，重設廣告容器上的大小。

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >當您收到全熒幕變更事件，並在廣告容器上設定新大小時，請依照以下步驟傳遞舞台顯示狀態，以確保播放器正確調整大小：
   >
   >```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
   >
