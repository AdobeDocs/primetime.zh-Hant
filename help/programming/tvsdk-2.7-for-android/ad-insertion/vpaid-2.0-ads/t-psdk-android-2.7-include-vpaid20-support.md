---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-title: 實作VPAID 2.0整合
title: 實作VPAID 2.0整合
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 25f97c8d296f71deddc8f9d12b97007ddf73f603
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%

---


# 實作VPAID 2.0整合{#implement-vpaid-integration}

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
   >在VPAID 2.0工作流程中，自訂廣告檢視必須跨`AdBreak`開始（事件`AD_BREAK_START`）和`AdBreak`完成（事件`AD_BREAK_COMPLETE`）維護您的`CustomAdView`例項，從您建立自訂廣告檢視到您處理廣告檢視時，都是如此。 也就是說，請勿在每個廣告插播開始時建立自訂廣告檢視，並在每個廣告插播結束時處置它。
   >
   >
   >此外，您只應在播放器處於「已準備」狀態時建立自訂廣告檢視，
   >
   >
   >只有在呼叫重設時，才能處理自訂廣告檢視。 例如：
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
   >最後，在處理自訂廣告檢視之前，您必須先從`FrameLayout`中移除它。 例如：
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
