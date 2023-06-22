---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的監聽器。
title: 實作VPAID 2.0整合
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 實作VPAID 2.0整合 {#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的監聽器。

若要新增VPAID 2.0支援：

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

1. 建立接聽程式並處理事件接聽程式中說明的事件。

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流程中，對於自訂廣告檢視，維護您的網站非常重要 `CustomAdView` 執行個體跨越 `AdBreak` 開始(事件 `AD_BREAK_START`)和 `AdBreak` 完成(事件 `AD_BREAK_COMPLETE`)，從您建立自訂廣告檢視到您處置它為止。 也就是說，請勿在每次廣告插播開始時建立自訂廣告檢視，並在每次廣告插播完成時將其處置。
   >
   >
   >此外，您應僅在播放器處於「已準備」狀態時建立自訂廣告檢視。
   >
   >
   >只有在呼叫重設時處置自訂廣告檢視。 例如：
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
   >最後，在處置自訂廣告檢視之前，您必須將其從 `FrameLayout`. 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
