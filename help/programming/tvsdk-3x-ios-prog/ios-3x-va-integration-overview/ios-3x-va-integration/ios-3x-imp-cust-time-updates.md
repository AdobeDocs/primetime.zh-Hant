---
description: 在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK的localTime值所報告位置不同的播放點位置。 例如，線上性資料流播放期間，每個程式的播放點可相對於其開始時間而提供。
title: 實作自訂時間更新
exl-id: df35d422-d9dc-496d-8f6f-cf34d82ab046
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# 實作自訂時間更新 {#implement-custom-time-updates}

在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK的localTime值所報告位置不同的播放點位置。 例如，線上性資料流播放期間，每個程式的播放點可相對於其開始時間而提供。

>[!TIP]
>
>唯有當您要提供與預設位置不同的播放點位置時，才能覆寫此方法。

覆寫預設播放點位置：

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>在此程式碼範例中，500隻是範例值。 您需要為自訂播放點位置使用不同的值。
