---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聽眾對象。
title: 實作VPAID 2.0整合
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 實作VPAID 2.0整合 {#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聽眾對象。

1. 當播放器處於「已準備」狀態時，將自訂廣告檢視新增到播放器介面。

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

1. 建立監聽器並處理中說明的事件 [活動](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流程中，對於自訂廣告檢視，維護您的網站非常重要 `CustomAdView` 例項跨 `AdBreak` 開始(事件 `AD_BREAK_START`)和 `AdBreak` 完成(事件 `AD_BREAK_COMPLETE`)，從您建立自訂廣告檢視到您處置它為止。 也就是說，請勿在每次廣告插播開始時建立自訂廣告檢視，並在每次廣告插播完成時將其處置。
   >
   >
   >此外，您應該只在播放器處於已準備狀態時，建立自訂廣告檢視，
   >
   >
   >只有在呼叫重設時處置自訂廣告檢視。 例如：
   >
   >```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >最後，在處置自訂廣告檢視之前，您必須將其從 `FrameLayout`. 例如：
   >
   >```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
