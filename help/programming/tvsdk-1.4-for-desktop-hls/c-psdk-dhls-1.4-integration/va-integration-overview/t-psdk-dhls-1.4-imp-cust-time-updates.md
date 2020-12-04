---
description: 在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK localTime值所報告的播放頭位置不同的播放頭位置。 例如，在LINEAR串流播放期間，可以相對於每個節目的開始時間提供其播放頭。
seo-description: 在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK localTime值所報告的播放頭位置不同的播放頭位置。 例如，在LINEAR串流播放期間，可以相對於每個節目的開始時間提供其播放頭。
seo-title: 實作自訂時間更新
title: 實作自訂時間更新
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 實施自訂時間更新{#implement-custom-time-updates}

在某些分析實作中，用戶端應用程式可能會想要提供與TVSDK localTime值所報告的播放頭位置不同的播放頭位置。 例如，在LINEAR串流播放期間，可以相對於每個節目的開始時間提供其播放頭。

>[!TIP]
>
>只有當您想要提供不同於預設位置的播放磁頭位置時，才覆寫此方法。

1. 要覆蓋預設播放頭位置：

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
   >此程式碼片段中的值僅為範例。 您需要針對自訂播放頭位置使用不同的值。

