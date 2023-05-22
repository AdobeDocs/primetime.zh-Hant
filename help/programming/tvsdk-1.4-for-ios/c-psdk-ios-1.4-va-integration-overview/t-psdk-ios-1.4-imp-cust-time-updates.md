---
description: 在某些分析實現中，客戶端應用程式可能希望提供與TVSDK的localTime值報告的位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於其開始時間提供每個節目的播放頭。
title: 實施自定義時間更新
exl-id: 85ec4744-541f-451f-95a3-063dd1151635
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 實施自定義時間更新{#implement-custom-time-updates}

在某些分析實現中，客戶端應用程式可能希望提供與TVSDK的localTime值報告的位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於其開始時間提供每個節目的播放頭。

>[!TIP]
>
>僅當要提供與預設位置不同的播放頭位置時，才覆蓋此方法。

1. 要覆蓋預設播放頭位置，請執行以下操作：

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >在此代碼示例中，500隻是示例值。 您需要為自定義播放頭位置使用其他值。
