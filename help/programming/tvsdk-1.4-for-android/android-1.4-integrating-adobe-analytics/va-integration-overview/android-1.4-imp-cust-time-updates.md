---
description: 在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK localTime值回報之位置不同的播放點位置。 例如，線上性資料流播放期間，每個程式的播放點可相對於其開始時間而提供。
title: 實作自訂時間更新
exl-id: 91e778ca-cdab-4c50-96f8-3333d210fd4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 實作自訂時間更新 {#implement-custom-time-updates}

在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK localTime值回報之位置不同的播放點位置。 例如，線上性資料流播放期間，每個程式的播放點可相對於其開始時間而提供。

>[!TIP]
>
>只有在您想提供預設位置以外的播放點位置時，才覆寫此方法。

覆寫預設播放點位置：

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
>此程式碼片段中的值僅為範例。 您需要對自訂播放點位置使用不同的值。
