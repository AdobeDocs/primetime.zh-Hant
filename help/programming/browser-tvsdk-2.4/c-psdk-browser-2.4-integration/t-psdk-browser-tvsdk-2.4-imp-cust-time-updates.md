---
description: 在某些分析實現中，客戶端應用程式可能希望提供與瀏覽器TVSDK localTime值報告的位置不同的播放頭位置。
title: 實施自定義時間更新
exl-id: 4d045c4d-298a-42ae-af61-0463a76bc872
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 實施自定義時間更新{#implement-custom-time-updates}

在某些分析實現中，客戶端應用程式可能希望提供與瀏覽器TVSDK localTime值報告的位置不同的播放頭位置。

例如，線上性流回放期間，可以相對於其開始時間提供每個節目的播放頭。

>[!TIP]
>
>僅當要提供除預設位置之外的播放頭位置時，才覆蓋此方法。

要覆蓋預設播放頭位置，請執行以下操作：

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>此代碼段中的值只是示例。 您需要為自定義播放頭位置使用不同的值。
