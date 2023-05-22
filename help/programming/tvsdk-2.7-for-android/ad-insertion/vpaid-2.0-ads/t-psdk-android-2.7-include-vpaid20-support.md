---
description: 要添加VPAID 2.0支援，請添加自定義廣告視圖和相應的偵聽器。
title: 實施VPAID 2.0整合
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 實施VPAID 2.0整合 {#implement-vpaid-integration}

要添加VPAID 2.0支援，請添加自定義廣告視圖和相應的偵聽器。

要添加VPAID 2.0支援，請執行以下操作：

1. 當播放器處於PREPARED狀態時，將自定義廣告視圖添加到播放器介面。

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. 建立偵聽器並處理事件偵聽器中描述的事件。

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流中，對於自定義廣告視圖，維護您的 `CustomAdView` 實例 `AdBreak` 啟動（事件） `AD_BREAK_START`) `AdBreak` 完成（事件） `AD_BREAK_COMPLETE`)，從建立自定義廣告視圖到處置自定義廣告視圖。 也就是說，不要在每個廣告中斷開始時建立自定義廣告視圖，並在每個廣告中斷完成時將其處置。
   >
   >
   >此外，您只應在播放器處於PREPARED狀態時建立自定義廣告視圖，
   >
   >
   >調用重置時僅處置自定義廣告視圖。 例如：
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >最後，在處理自定義廣告視圖之前，必須將其從 `FrameLayout`。 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
