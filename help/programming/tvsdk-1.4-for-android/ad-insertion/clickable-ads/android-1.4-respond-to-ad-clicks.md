---
description: 當使用者點選廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供點按的目的地URL相關資訊。
title: 回應廣告的點按
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# 回應廣告的點按{#respond-to-clicks-on-ads}

當使用者點選廣告或相關按鈕時，您的應用程式必須回應。 TVSDK會提供點按的目的地URL相關資訊。

1. 若要設定TVSDK的事件監聽器，並提供點進資訊，請註冊 `AdClickedEventListener.onAdClicked`.

   當使用者點按廣告或相關按鈕時，TVSDK會傳送此通知，包括點按目的地的相關資訊。
1. 監視使用者在可點按廣告上的互動。
1. 當使用者觸控或點選廣告或按鈕，要通知TVSDK，請呼叫 `notifyClick` 於 `MediaPlayerView`.
1. 聆聽 `onAdClick(AdClickEvent event)` TVSDK的事件。
1. 若要擷取點進URL和相關資訊，請使用 `AdClickEvent` 執行個體。
1. 暫停視訊。

   如需有關暫停視訊的詳細資訊，請參閱 [暫停並繼續播放。](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. 使用點進資訊來顯示廣告點進URL和相關資訊。

       例如，您可以用下列其中一種方式來顯示資訊：
   
   * 在您的應用程式中，在瀏覽器中開啟點進URL。

     在案頭平台上，視訊廣告播放區域是用來在使用者點按時叫用點進URL。
   * 將使用者重新導向至其外部行動網頁瀏覽器。

     在行動裝置上，視訊廣告播放區域可用於其他功能，例如隱藏和顯示控制項、暫停播放、展開至全熒幕等。 在這些裝置上，會使用個別檢視（例如贊助者按鈕）來啟動點進URL。

1. 關閉顯示點進資訊的瀏覽器視窗，然後繼續播放視訊。

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

例如：

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
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
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
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
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
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
