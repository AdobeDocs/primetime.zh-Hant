---
description: TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。
title: 可點選廣告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# 可點選廣告{#clickable-ads}

TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。

針對「Flash執行階段」的TVSDK，只有線性廣告可點選。

## 回應廣告的點按次數{#respond-to-clicks-on-ads}

當使用者按一下廣告或相關按鈕時，您的應用程式會負責回應。 TVSDK會提供您目標URL的相關資訊。

此範例顯示管理廣告點按的一種可能方式。

1. 每次播放廣告時，在媒體播放器上方顯示一個按鈕。 點按廣告的使用者會重新導向至廣告URL。 此按鈕是[!DNL ClickableAdsOverlay.xml]的一部分。

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

1. 在我們的媒體播放器範例[!DNL psdkdemo.xml]中加入此覆蓋。

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. 若要讓檢視僅在廣告播放時顯示，請監聽`onAdStart`和`onAdComplete`事件，由傳送。

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

1. 在可點選廣告上監控使用者互動。 當使用者觸碰或按一下廣告或按鈕時，請以`notifyClick`通知TVSDK。

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. 監聽`AdclickEvent.AD_CLICK`事件。

   如果廣告正在播放，TVSDK會調度`AdClickEvent.AD_CLICK`事件，您可從中擷取點進URL和相關資訊。

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. 在引導使用者至廣告URL時暫停媒體播放器。

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. 顯示廣告點進URL和任何相關資訊。

       例如，您可透過下列其中一種方式來顯示它：
   
   * 在您應用程式的瀏覽器中開啟點進URL。

      在案頭平台上，視訊廣告播放區域通常用於在使用者點按時叫用點進URL。
   * 將使用者重新導向至外部行動網頁瀏覽器。

      在行動裝置上，視訊廣告播放區域用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全螢幕等。 因此，在行動裝置上，通常會以個別檢視（例如贊助者按鈕）的方式，向使用者顯示點進URL。

1. 關閉顯示點進資訊的瀏覽器視窗，然後繼續播放視訊。
