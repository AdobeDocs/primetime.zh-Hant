---
description: TVSDK會提供您資訊，方便您對點進廣告採取行動。 當您建立播放器UI時，必須決定當使用者點按可點按廣告時如何回應。
title: 可點按的廣告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 可點按的廣告 {#clickable-ads}

TVSDK會提供您資訊，方便您對點進廣告採取行動。 當您建立播放器UI時，必須決定當使用者點按可點按廣告時如何回應。

對於Flash執行階段的TVSDK，只能點選線性廣告。

## 回應廣告的點按 {#respond-to-clicks-on-ads}

當使用者按一下廣告或相關按鈕時，您的應用程式將負責回應。 TVSDK可提供目的地URL的相關資訊。

此範例顯示管理廣告點按的一個可能方式。

1. 每次播放廣告時，都會在媒體播放器上方顯示一個按鈕。 按一下廣告的使用者會重新導向至廣告URL。 此按鈕是 [!DNL ClickableAdsOverlay.xml].

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

1. 將此覆蓋圖加入我們的媒體播放器範例、 [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. 若要讓檢視只在播放廣告時可見，請聆聽 `onAdStart` 和 `onAdComplete` 由傳送的事件。

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

1. 監視使用者在可點按廣告上的互動。 當使用者觸控或點選廣告或按鈕，通知TVSDK使用 `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. 聆聽 `AdclickEvent.AD_CLICK` 事件。

   如果廣告正在播放，TVSDK會傳送 `AdClickEvent.AD_CLICK` 事件，您可從中擷取點進URL和相關資訊。

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. 將使用者導向至廣告URL時暫停媒體播放器。

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. 顯示廣告點進URL及任何相關資訊。

       例如，您可以用下列其中一種方式來顯示它：
   
   * 在應用程式的瀏覽器中開啟點進URL。

     在案頭平台上，視訊廣告播放區域通常用於在使用者點按時叫用點進URL。
   * 將使用者重新導向至外部行動網頁瀏覽器。

     在行動裝置上，視訊廣告播放區域可用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全熒幕等。 因此，在行動裝置上，通常會向使用者顯示獨立的檢視（例如贊助者按鈕），作為啟動點進URL的方法。

1. 關閉顯示點進資訊的瀏覽器視窗，然後繼續播放視訊。
