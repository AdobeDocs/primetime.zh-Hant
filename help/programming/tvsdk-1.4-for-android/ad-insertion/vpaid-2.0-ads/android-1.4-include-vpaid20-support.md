---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的聆聽器。
title: 實作VPAID 2.0整合
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
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

