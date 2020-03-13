---
description: 當使用者點按廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供您點按之目標URL的相關資訊。
seo-description: 當使用者點按廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供您點按之目標URL的相關資訊。
seo-title: 回應廣告的點按次數
title: 回應廣告的點按次數
uuid: 58efaba5-d0f6-4ddd-9628-6bc065cc95d8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 回應廣告的點按次數 {#respond-to-clicks-on-ads}

TVSDK會提供您資訊，讓您能夠對點進式廣告採取行動。 當您建立播放器UI時，您必須決定當使用者點按可點按的廣告時如何回應。

對於Android專用的TVSDK，只有線性廣告可點選。
當使用者點按廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供您點按之目標URL的相關資訊。

1. 若要設定TVSDK的事件接聽程式，並提供點進資訊，請註冊 `AdClickedEventListener.onAdClicked`。

   當使用者點按廣告或相關按鈕時，TVSDK會派單此通知，包括點按目的地的相關資訊。
1. 在可點選廣告上監控使用者互動。
1. 當使用者觸碰或按一下廣告或按鈕時，若要通知TVSDK，請 `notifyClick` 呼叫 `MediaPlayerView`。
1. 聽取TVSDK `onAdClick(AdClickEvent event)` 的活動。
1. 若要擷取點進URL和相關資訊，請使用例項的getter方 `AdClickEvent` 法。
1. 暫停影片。

   如需暫停視訊的詳細資訊，請參閱「暫停——繼續播放」。
1. 使用點進資訊來顯示廣告點進URL及相關資訊。

       例如，您可以以下列其中一種方式顯示資訊：
   
   * 在您的應用程式中，在瀏覽器中開啟點進URL。

      在案頭平台上，視訊廣告播放區域用於在使用者點按時叫用點進URL。
   * 將使用者重新導向至其外部行動網頁瀏覽器。

      在行動裝置上，視訊廣告播放區域用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全螢幕等。 在這些裝置上，會使用個別的檢視（例如贊助者按鈕）來啟動點進URL。

1. 關閉顯示點進資訊的瀏覽器視窗，然後繼續播放視訊。

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

例如：

```java
private AdStartedEventListener adStartedEventListener =  
  new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener =  
  new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener =  
  new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
    } 
}; 
```

