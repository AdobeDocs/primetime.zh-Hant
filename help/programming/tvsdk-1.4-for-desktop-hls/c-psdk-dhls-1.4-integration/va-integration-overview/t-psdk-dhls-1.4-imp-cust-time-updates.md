---
description: 在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK localTime值所回報位置不同的播放點位置。 例如，在LINEAR串流播放期間，每個程式的播放點都可以相對於其開始時間來提供。
title: 實作自訂時間更新
exl-id: be0f2684-6a17-4d99-8875-7f404ce8a656
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 實作自訂時間更新{#implement-custom-time-updates}

在某些Analytics實作中，使用者端應用程式可能會想要提供與TVSDK localTime值所回報位置不同的播放點位置。 例如，在LINEAR串流播放期間，每個程式的播放點都可以相對於其開始時間來提供。

>[!TIP]
>
>唯有當您想提供預設位置以外的其他播放點位置時，才能覆寫此方法。

1. 覆寫預設播放點位置：

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
   >此程式碼片段中的值僅為範例。 您需要對自訂播放點位置使用不同的值。
