---
description: 在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK的localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。
seo-description: 在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK的localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。
seo-title: 實作自訂時間更新
title: 實作自訂時間更新
uuid: 174937ca-3c26-4385-a298-8a01fc93ea20
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 實作自訂時間更新 {#implement-custom-time-updates}

在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK的localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。

>[!TIP]
>
>只有在您想要提供不同於預設位置的播放磁頭位置時，才會覆寫此方法。

要覆蓋預設播放頭位置：

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>在此程式碼範例中，500隻是範例值。 您需要為自訂播放頭位置使用不同的值。