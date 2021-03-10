---
description: 瀏覽器TVSDK程式庫的通知部分可讓您建立記錄與除錯系統，以便用於診斷與驗證。
title: 通知系統
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 通知系統{#notification-system}

瀏覽器TVSDK程式庫的通知部分可讓您建立記錄與除錯系統，以便用於診斷與驗證。

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

瀏覽器TVSDK的API有&#x200B;*no throw*&#x200B;原則。 大部分方法會傳回`PSDKErrorCode`值，以指出方法是否成功執行。 如需所有可能`PSDKErrorCode`值的完整清單，請參閱瀏覽器TVSDK API參考。

非同步錯誤會透過特定事件通知。

瀏覽器TVSDK會派單`MediaPlayer`事件，以提供播放器活動的相關資訊。 您必須實作事件監聽器，才能擷取並回應這些事件。

>[!TIP]
>
>關鍵事件和資訊會記錄在網頁瀏覽器主控台上。

## 監聽通知{#section_06B96633433D497E842FB7ADD5F2C7DA}

您可以監聽通知，並將自己的通知新增至通知歷史記錄。 瀏覽器TVSDK通知系統的核心是`Notification`類別，代表單機通知。

若要設定您的應用程式以監聽通知：

1. 使用MediaPlayer例項來監聽MediaPlayer狀態變更。

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 實作回呼。

   回呼會接收`AdobePSDK.MediaPlayerStatusChangeEvent`的例項，而Browser TVSDK會將此事件物件傳遞至包含新播放器狀態的回呼。
1. 您的應用程式可監聽瀏覽器TVSDK透過`MediaPlayer`例項傳送的其他事件。

