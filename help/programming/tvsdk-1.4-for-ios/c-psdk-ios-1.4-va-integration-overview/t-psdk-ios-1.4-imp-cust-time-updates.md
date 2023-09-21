---
description: 在某些分析實作中，使用者端應用程式可能會想要提供與TVSDK的localTime值所回報位置不同的播放點位置。 例如，線上性資料流播放期間，每個節目的播放點可相對於其開始時間來提供。
title: 實作自訂時間更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 實作自訂時間更新{#implement-custom-time-updates}

在某些分析實作中，使用者端應用程式可能會想要提供與TVSDK的localTime值所回報位置不同的播放點位置。 例如，線上性資料流播放期間，每個節目的播放點可相對於其開始時間來提供。

>[!TIP]
>
>只有在您想提供不同於預設位置的播放點位置時，才能覆寫此方法。

1. 覆寫預設播放點位置：

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >在此程式碼範例中，500隻是一個範例值。 您需要為自訂播放點位置使用不同的值。
