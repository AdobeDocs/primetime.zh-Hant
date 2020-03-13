---
description: 您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。
seo-description: 您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。
seo-title: 儲存視訊位置並稍後繼續
title: 儲存視訊位置並稍後繼續
uuid: 03ed5c63-008d-4dd1-9a31-baefa73b56e2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 儲存視訊位置並稍後繼續{#save-the-video-position-and-resume-later}

您可以儲存視訊中目前的播放位置，並在未來作業中在相同位置繼續播放。

動態插入的廣告在使用者工作階段間不同，因此 **使用拼接** 的廣告來儲存位置，是指未來工作階段中的不同位置。 TVSDK提供在忽略拼接廣告時擷取播放位置的方法。

1. 當使用者結束視訊時，您的應用程式會擷取並儲存視訊中的位置。

   >[!TIP]
   >
   >廣告期間不包含在內。

   由於廣告模式、頻率上限設定等原因，每個工作階段的廣告插播都會有所不同。 視訊在某個作業中的目前時間在未來作業中可能不同。 在視訊中儲存位置時，應用程式會擷取本機時間。 使用 `localTime` 屬性讀取此位置，您可將其保存在設備上或伺服器上的資料庫中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果使用者是視訊的第20分鐘，而此位置包含5分鐘廣告，則 `currentTime``be` 為1200秒，而 `localTime` 此位置為 `be` 900秒。

1. 當播放器活動繼續時，還原使用者工作階段。

   TVSDK不會在TVSDK初始化之間繼續播放，因為它不會在本機儲存任何資訊。 您的應用程式必須實作此邏輯。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 要在相同位置繼續視頻：

   * 若要從先前作業儲存的位置繼續播放視訊，請使用 `seekToLocal`。

      >[!TIP]
      >
      >此方法僅與本機時間值一起呼叫。 如果以目前的時間結果呼叫方法，就會發生錯誤行為。

   * 若要尋找目前的時間，請使用 `seek`。

1. 當您的應用程式收到狀 `onStatusChanged` 態變更事件時，請尋找儲存的本機時間。
1. 依照廣告原則介面中的指定，提供廣告分段。
1. 延伸預設廣告原則選擇器，以實作自訂廣告原則選擇器。
1. 透過實作，提供必須向使用者呈現的廣告插頁 `selectAdBreaksToPlay`。

   當播放器進入PREPARED狀態時，所有廣告都已解析，因此屬性會在 `AdPolicyInfo.adBreakTimelineItem` 當地時間位置之前包含所有廣告分段。 您的應用程式可決定播放前段廣告插播並繼續到指定的當地時間、播放中段廣告插播並繼續到指定的當地時間，或不播放廣告插播。
