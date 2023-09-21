---
description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo，TVSDK不會發出錯誤。 您的應用程式可藉由接聽StageVideoAvailabilityEvent來判斷StageVideo是否可用。
title: 檢查StageVideo是否可用
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo，TVSDK不會發出錯誤。 您的應用程式可藉由接聽StageVideoAvailabilityEvent來判斷StageVideo是否可用。

從Flash15和更新版本，當硬體 `StageVideo` 無法使用，它將回覆至軟體 `StageVideo`. 對於Flash14和更早版本，您可以確定 `StageVideo` 可用。 如果 `StageVideo` 無法使用，您可以使用 `StageVideoAvailabilityEvent` 以瞭解無法使用的原因。

1. 聆聽 `StageVideoAvailabilityEvent` 以判斷是否 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 無法使用，請核取 `flash.media.StageVideoAvailabilityReason`.
