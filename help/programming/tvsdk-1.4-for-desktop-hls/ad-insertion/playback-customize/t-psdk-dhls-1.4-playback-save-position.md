---
description: 您可以將目前的播放位置儲存在視訊中，並在未來工作階段的相同位置繼續播放。
title: 儲存視訊位置並稍後繼續
exl-id: a06897a6-bf57-4902-b1b4-e931419b56ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 儲存視訊位置並稍後繼續{#save-the-video-position-and-resume-later}

您可以將目前的播放位置儲存在視訊中，並在未來工作階段的相同位置繼續播放。

動態插入的廣告會因使用者工作階段而異，所以儲存位置 **替換為** 拼接廣告是指未來工作階段中的不同位置。 TVSDK提供在忽略拼接廣告時擷取播放位置的方法。

1. 當使用者結束視訊時，您的應用程式會擷取並儲存視訊中的位置。

   >[!TIP]
   >
   >不包括廣告持續時間。

   由於廣告模式、頻率上限等原因，每個工作階段的廣告插播可能會有所不同。 一個工作階段中視訊的目前時間，可能會與未來工作階段中的不同。 在視訊中儲存位置時，應用程式會擷取當地時間。 使用 `localTime` 屬性來讀取此位置，您可以將其儲存在裝置上或伺服器的資料庫中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果使用者在影片的第20分鐘，而此位置包含五分鐘的廣告， `currentTime` 將 `be` 1200秒，而 `localTime` 在此位置將會 `be` 900秒。

1. 播放器活動繼續時還原使用者工作階段。

   TVSDK不會在TVSDK初始化之間繼續播放，因為它不會將任何資訊儲存在本機。 您的應用程式必須實作此邏輯。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 若要在相同位置繼續播放視訊：

   * 若要從先前工作階段儲存的位置繼續播放視訊，請使用 `seekToLocal`.

      >[!TIP]
      >
      >此方法只會以本機時間值呼叫。 如果使用目前時間結果呼叫方法，則會發生錯誤行為。

   * 若要搜尋到目前時間，請使用 `seek`.

1. 當您的應用程式收到 `onStatusChanged` 狀態變更事件，搜尋已儲存的當地時間。
1. 提供廣告原則介面中指定的廣告插播。
1. 擴充預設廣告原則選擇器，實作自訂廣告原則選擇器。
1. 透過實作，提供必須呈現給使用者的廣告插播 `selectAdBreaksToPlay`.

   當播放器進入「已準備」狀態時，所有廣告均已解決，因此 `AdPolicyInfo.adBreakTimelineItem` 屬性包含所有在本機時間位置之前的廣告插播。 您的應用程式可以決定播放前段廣告插播並繼續到指定的當地時間、播放中段廣告插播並繼續到指定的當地時間，或不播放任何廣告插播。
