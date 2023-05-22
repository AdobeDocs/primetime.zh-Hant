---
description: 在某些分析實現中，客戶端應用程式可能希望提供與TVSDK localTime值報告的播放頭位置不同的播放頭位置。 例如，在LINEAR流回放期間，可以相對於每個節目的開始時間提供每個節目的播放頭。
title: 實施自定義時間更新
exl-id: be0f2684-6a17-4d99-8875-7f404ce8a656
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 實施自定義時間更新{#implement-custom-time-updates}

在某些分析實現中，客戶端應用程式可能希望提供與TVSDK localTime值報告的播放頭位置不同的播放頭位置。 例如，在LINEAR流回放期間，可以相對於每個節目的開始時間提供每個節目的播放頭。

>[!TIP]
>
>僅當要提供與預設位置不同的播放頭位置時，才覆蓋此方法。

1. 要覆蓋預設播放頭位置，請執行以下操作：

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >此代碼段中的值只是示例。 您需要為自定義播放頭位置使用不同的值。
