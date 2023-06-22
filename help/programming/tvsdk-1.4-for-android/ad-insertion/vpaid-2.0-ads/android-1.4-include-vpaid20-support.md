---
description: 若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的監聽器。
title: 實作VPAID 2.0整合
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 實作VPAID 2.0整合{#implement-vpaid-integration}

若要新增VPAID 2.0支援，請新增自訂廣告檢視和適當的監聽器。

若要新增VPAID 2.0支援：

1. 將自訂廣告檢視新增至播放器介面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 新增自訂廣告事件的接聽程式。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

