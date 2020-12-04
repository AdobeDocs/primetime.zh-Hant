---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
seo-title: 實作VPAID 2.0整合
title: 實作VPAID 2.0整合
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# 實作VPAID 2.0整合{#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。

若要新增VPAID 2.0支援：

1. 將自訂廣告檢視新增至播放器介面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 新增自訂廣告事件的監聽器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

