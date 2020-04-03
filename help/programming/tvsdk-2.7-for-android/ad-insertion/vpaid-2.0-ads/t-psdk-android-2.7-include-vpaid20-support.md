---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-title: 實作VPAID 2.0整合
title: 實作VPAID 2.0整合
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 實作VPAID 2.0整合 {#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。

若要新增VPAID 2.0支援：

1. 當播放器處於「已準備」狀態時，將自訂廣告檢視新增至播放器介面。

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

1. 建立偵聽程式並處理事件偵聽程式中描述的事件。

   >[!IMPORTANT]
   >
   >在VPAID 2.0工作流程中，自訂廣告檢視的執行個體，從您建立自訂廣告檢視到您處理廣告檢視時，在開始(事件 `CustomAdView` )和結束(事件 `AdBreak``AD_BREAK_START``AdBreak``AD_BREAK_COMPLETE`)之間維持執行個體非常重要。 也就是說，請勿在每個廣告插播開始時建立自訂廣告檢視，並在每個廣告插播結束時處置它。
   >
   >
   >此外，您只應在播放器處於「已準備」狀態時建立自訂廣告檢視，
   >
   >
   >只有在呼叫重設時，才能處理自訂廣告檢視。 例如：
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
   >最後，在您處理自訂廣告檢視之前，您必須先將它從中移除 `FrameLayout`。 例如：
   >
   >```
   >if (_playerFrame != null) 
   >   _playerFrame.removeAllViews(); 
   >```
