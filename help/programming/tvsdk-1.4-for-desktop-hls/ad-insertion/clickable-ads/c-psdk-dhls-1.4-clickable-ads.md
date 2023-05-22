---
description: TVSDK提供資訊，以便您能夠對點擊廣告進行操作。 在建立播放器UI時，必須決定當用戶按一下可按一下廣告時如何響應。
title: 可點擊的廣告
exl-id: 50c74c82-c5d8-43f6-accf-8330a426a7bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 可點擊的廣告 {#clickable-ads}

TVSDK提供資訊，以便您能夠對點擊廣告進行操作。 在建立播放器UI時，必須決定當用戶按一下可按一下廣告時如何響應。

對於Flash運行時的TVSDK，只有線性廣告可點擊。

## 響應廣告點擊 {#respond-to-clicks-on-ads}

當用戶按一下廣告或相關按鈕時，您的應用程式負責響應。 TVSDK提供有關目標URL的資訊。

此示例顯示了一種管理廣告點擊的可能方法。

1. 每次播放廣告時，在媒體播放器的頂部顯示按鈕。 按一下廣告的用戶被重定向到廣告URL。 此按鈕是 [!DNL ClickableAdsOverlay.xml]。

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. 在媒體播放器示例中加入此覆蓋， [!DNL psdkdemo.xml]。

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. 要僅在播放廣告時使視圖可見，請收聽 `onAdStart` 和 `onAdComplete` 由發送的事件。

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. 監視可點擊廣告上的用戶交互。 當用戶觸摸或按一下廣告或按鈕時，通知TVSDK `notifyClick`。

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. 聽著 `AdclickEvent.AD_CLICK` 的子菜單。

   如果播放廣告，TVSDK將 `AdClickEvent.AD_CLICK` 事件，您可以從中檢索按一下瀏覽URL和相關資訊。

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. 暫停媒體播放器，同時將用戶引導到廣告URL。

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. 顯示廣告點擊URL和任何相關資訊。

       例如，可以通過以下方式之一顯示它：
   
   * 在應用程式內的瀏覽器中開啟點擊式URL。

      在案頭平台上，視頻和播放區域通常用於在用戶按一下時調用點擊式URL。
   * 將用戶重定向到外部移動Web瀏覽器。

      在移動設備上，視頻和播放區域用於其他功能，如隱藏和顯示控制項、暫停播放、擴展到全屏等。 因此，在移動設備上，通常會向用戶顯示單獨的視圖（如贊助者按鈕），作為啟動點擊式URL的手段。

1. 關閉其中顯示點擊資訊的瀏覽器窗口並繼續播放視頻。
