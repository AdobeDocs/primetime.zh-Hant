---
description: 要添加VPAID 2.0支援，請添加自定義廣告視圖和相應的偵聽器。
title: 實施VPAID 2.0整合
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# 實施VPAID 2.0整合{#implement-vpaid-integration}

要添加VPAID 2.0支援，請添加自定義廣告視圖和相應的偵聽器。

要添加VPAID 2.0支援，請執行以下操作：

1. 將自定義廣告視圖添加到播放器介面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 為自定義廣告事件添加偵聽器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

