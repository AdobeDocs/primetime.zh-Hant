---
description: 在某些分析實作中，用戶端應用程式可能會想提供與TVSDK localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。
seo-description: 在某些分析實作中，用戶端應用程式可能會想提供與TVSDK localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。
seo-title: 實作自訂時間更新
title: 實作自訂時間更新
uuid: 7f5d46e5-eab6-4bdc-b015-ae27ddb609ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 實作自訂時間更新 {#implement-custom-time-updates}

在某些分析實作中，用戶端應用程式可能會想提供與TVSDK localTime值所報告位置不同的播放頭位置。 例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。

>[!TIP]
>
>只有在您想要提供預設位置以外的播放磁頭位置時，才會覆寫此方法。

要覆蓋預設播放頭位置：

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>此程式碼片段中的值僅為範例。 您需要針對自訂播放頭位置使用不同的值。