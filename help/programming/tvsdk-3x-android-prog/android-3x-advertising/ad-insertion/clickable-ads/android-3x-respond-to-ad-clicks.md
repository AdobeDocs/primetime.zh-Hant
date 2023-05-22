---
description: 當用戶按一下廣告或相關按鈕時，您的應用程式必須做出響應。 TVSDK提供有關按一下的目標URL的資訊。
title: 響應廣告點擊
exl-id: 14716265-747d-4472-801e-2b97c7df2425
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 響應廣告點擊 {#respond-to-clicks-on-ads}

TVSDK提供資訊，以便您能夠對點擊廣告進行操作。 在建立播放器UI時，必須決定當用戶按一下可按一下廣告時如何響應。

對於Android版TVSDK，只有線性廣告可點擊。
當用戶按一下廣告或相關按鈕時，您的應用程式必須做出響應。 TVSDK提供有關按一下的目標URL的資訊。

1. 要為TVSDK設定事件偵聽器，並提供點擊資訊，請註冊 `AdClickedEventListener.onAdClicked`。

   當用戶按一下廣告或相關按鈕時，TVSDK將調度此通知，包括有關按一下的目標的資訊。
1. 監視可點擊廣告上的用戶交互。
1. 當用戶觸摸或按一下廣告或按鈕時，要通知TVSDK，請撥打 `notifyClick` 的 `MediaPlayerView`。
1. 聽著 `onAdClick(AdClickEvent event)` TVSDK中的事件。
1. 要檢索點擊式URL和相關資訊，請使用 `AdClickEvent` 實例。
1. 暫停視頻。

   有關暫停視頻的詳細資訊，請參閱  [暫停並繼續播放](../../ad-insertion/clickable-ads/android-3x-pausing-resuming-playback.md)。
1. 使用點擊資訊顯示廣告點擊URL和相關資訊。 例如，可以通過以下方式之一顯示資訊：

   * 在應用程式中，通過在瀏覽器中開啟點擊式URL。

      在案頭平台上，視頻和播放區域用於在用戶點擊時調用點擊式URL。
   * 將用戶重定向到其外部移動Web瀏覽器。

      在移動設備上，視頻和播放區域用於其他功能，如隱藏和顯示控制項、暫停播放、擴展到全屏等。 在這些設備上，使用單獨的視圖（如發起人按鈕）來啟動點擊式URL。

1. 關閉其中顯示點擊資訊的瀏覽器窗口並繼續播放視頻。

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
