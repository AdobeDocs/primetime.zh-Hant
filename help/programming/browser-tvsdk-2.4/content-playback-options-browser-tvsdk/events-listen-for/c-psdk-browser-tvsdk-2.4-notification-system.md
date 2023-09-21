---
description: 瀏覽器TVSDK程式庫的通知部分可讓您建立可用於診斷和驗證目的的記錄與偵錯系統。
title: 通知系統
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 通知系統 {#notification-system}

瀏覽器TVSDK程式庫的通知部分可讓您建立可用於診斷和驗證目的的記錄與偵錯系統。

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

瀏覽器TVSDK具有 *no throw* 其API的原則。 大部分方法會傳回 `PSDKErrorCode` 表示方法是否成功執行的值。 如需所有可能的完整清單 `PSDKErrorCode` 值，請參閱瀏覽器TVSDK API參考。

系統會透過特定事件通知非同步錯誤。

瀏覽器TVSDK傳送作業 `MediaPlayer` 事件，以提供播放器活動的相關資訊。 您必須實作事件接聽程式來擷取和回應這些事件。

>[!TIP]
>
>重要事件和資訊會記錄在網頁瀏覽器主控台上。

## 接聽通知 {#section_06B96633433D497E842FB7ADD5F2C7DA}

您可以接聽通知，並將您自己的通知新增至通知歷史記錄。 瀏覽器TVSDK通知系統的核心為 `Notification` 類別，代表獨立通知。

若要設定應用程式以接聽通知，請執行下列動作：

1. 使用MediaPlayer例項接聽MediaPlayer狀態變更。

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 實作回呼。

   回呼會接收 `AdobePSDK.MediaPlayerStatusChangeEvent`，且瀏覽器TVSDK會將此事件物件傳遞至包含新播放器狀態的回呼。
1. 您的應用程式可監聽由瀏覽器TVSDK傳送的其他事件，方法是使用 `MediaPlayer` 執行個體。
