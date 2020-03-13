---
description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。
seo-description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。
seo-title: 檢查StageVideo是否可用
title: 檢查StageVideo是否可用
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。

從Flash 15和更新版本開始，當硬 `StageVideo` 體不提供時，就會回歸軟體 `StageVideo`。 對於Flash 14和舊版軟體，您可以決定是否 `StageVideo` 可用。 如果 `StageVideo` 無法使用，您可以使用來 `StageVideoAvailabilityEvent` 瞭解為何無法使用。

1. 監聽以 `StageVideoAvailabilityEvent` 確定是否 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 不可用，請檢查 `flash.media.StageVideoAvailabilityReason`。
