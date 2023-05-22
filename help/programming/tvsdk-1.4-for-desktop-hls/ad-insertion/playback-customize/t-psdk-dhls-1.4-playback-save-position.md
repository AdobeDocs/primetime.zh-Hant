---
description: 您可以保存視頻中的當前播放位置，並在將來的會話中在相同位置繼續播放。
title: 保存視頻位置，稍後繼續
exl-id: a06897a6-bf57-4902-b1b4-e931419b56ba
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 保存視頻位置，稍後繼續{#save-the-video-position-and-resume-later}

您可以保存視頻中的當前播放位置，並在將來的會話中在相同位置繼續播放。

動態插入的廣告在用戶會話之間不同，因此保存位置 **與** 拼接廣告是指將來會話中的不同位置。 TVSDK提供了在忽略拼接廣告時檢索回放位置的方法。

1. 當用戶退出視頻時，應用程式將檢索並保存視頻中的位置。

   >[!TIP]
   >
   >不包括廣告持續時間。

   由於廣告模式、頻率封頂等原因，廣告中斷在每個會話中都可能會有所不同。 視頻在一個會話中的當前時間在未來會話中可能不同。 當在視頻中保存位置時，應用程式檢索本地時間。 使用 `localTime` 用於讀取此位置的屬性，您可以將此位置保存在設備上或伺服器上的資料庫中。

   ```
   var resumeTime:Number = player.localTime; 
   // save the resumeTime to a persistent location
   ```

   例如，如果用戶在視頻的第20分鐘，而此位置包含5分鐘的廣告， `currentTime` 會 `be` 1200秒，而 `localTime` 在這個位置 `be` 900秒。

1. 播放器活動恢復時還原用戶會話。

   TVSDK不會在TVSDK初始化之間恢復回放，因為它不會在本地保存任何資訊。 您的應用程式必須實現此邏輯。

   ```
   // retrieve the resumeTime from the persistent location 
   var resumeTime:Number:Number = ...;
   ```

1. 要在同一位置恢復視頻：

   * 要從上次會話中保存的位置繼續播放視頻，請使用 `seekToLocal`。

      >[!TIP]
      >
      >此方法僅使用本地時間值調用。 如果使用當前時間結果調用方法，則會發生錯誤行為。

   * 要查找當前時間，請使用 `seek`。

1. 當您的應用程式收到 `onStatusChanged` 狀態更改事件，查找已保存的本地時間。
1. 提供在廣告策略介面中指定的廣告分段。
1. 通過擴展預設廣告策略選擇器來實現自定義廣告策略選擇器。
1. 通過實現，提供必須向用戶顯示的廣告分段 `selectAdBreaksToPlay`。

   當玩家進入PREPARED狀態時，所有廣告都已解析，因此 `AdPolicyInfo.adBreakTimelineItem` 屬性包含本地時間位置之前的所有廣告分段。 您的應用程式可以決定播放預播廣告中斷，然後繼續到指定的本地時間，播放中播廣告中斷，然後繼續到指定的本地時間，或者不播放廣告中斷。
