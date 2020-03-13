---
description: 在某些分析實作中，用戶端應用程式可能會想要提供與瀏覽器TVSDK localTime值所報告位置不同的播放頭位置。
seo-description: 在某些分析實作中，用戶端應用程式可能會想要提供與瀏覽器TVSDK localTime值所報告位置不同的播放頭位置。
seo-title: 實作自訂時間更新
title: 實作自訂時間更新
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 實作自訂時間更新{#implement-custom-time-updates}

在某些分析實作中，用戶端應用程式可能會想要提供與瀏覽器TVSDK localTime值所報告位置不同的播放頭位置。

例如，線上性流回放期間，可以相對於每個節目的開始時間提供節目的播放頭。

>[!TIP]
>
>只有在您想要提供預設位置以外的播放磁頭位置時，才會覆寫此方法。

要覆蓋預設播放頭位置：

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>此程式碼片段中的值僅為範例。 您需要針對自訂播放頭位置使用不同的值。

