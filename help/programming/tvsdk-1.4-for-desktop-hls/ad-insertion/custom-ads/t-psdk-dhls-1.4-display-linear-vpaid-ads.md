---
description: TVSDK支援在廣告分段中顯示線性視頻播放器 — 廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版還可以與Browser TVSDK和JavaScript配合使用。
title: 在廣告時段顯示線性VPAID廣告
exl-id: 316a38ac-ec2d-498c-b441-304e2fa75993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 在廣告時段顯示線性VPAID廣告{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK支援在廣告分段中顯示線性視頻播放器 — 廣告介面定義(VPAID)廣告。 VPAID 1.0版需要Flash，而2.0版還可以與Browser TVSDK和JavaScript配合使用。

要正確顯示VPAID廣告，必須提供廣告容器( `AdContainerView`) `MediaPlayerContext` 實例。

VPAID廣告的限制：

* VPAID廣告不一定具有預定的持續時間，因為廣告可以是互動的。 因此，廣告持續時間（由廣告伺服器響應定義）可能並不總是與廣告的真實持續時間完全對應。
* 對於VPAID 1.0廣告，TVSDK要求在設備上安裝Flash播放器14.0.0.160或更高版本。 對於Flash播放器的早期版本，禁用此功能並跳過VPAID 1.0廣告。

要設定廣告容器，以便在廣告分段內顯示VPAID廣告（版本1.0或2.0）:

1. 使用以下示例代碼設定可顯示VPAID廣告的廣告容器。

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

1. 當視圖調整大小時，重置廣告容器上的大小。

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >在獲得全屏更改事件並在廣告容器上設定新大小時，按如下方式傳遞舞台顯示狀態，以確保播放器的大小正確調整：
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
