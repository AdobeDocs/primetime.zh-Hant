---
description: 在某些Analytics實作中，使用者端應用程式可能會想要提供與瀏覽器TVSDK localTime值回報之位置不同的播放點位置。
title: 實作自訂時間更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 實作自訂時間更新{#implement-custom-time-updates}

在某些Analytics實作中，使用者端應用程式可能會想要提供與瀏覽器TVSDK localTime值回報之位置不同的播放點位置。

例如，線上性資料流播放期間，每個節目的播放點可相對於其開始時間來提供。

>[!TIP]
>
>只有在您想提供預設位置以外的播放點位置時，才覆寫此方法。

覆寫預設播放點位置：

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>此程式碼片段中的值僅為範例。 您需要為自訂播放點位置使用不同的值。
