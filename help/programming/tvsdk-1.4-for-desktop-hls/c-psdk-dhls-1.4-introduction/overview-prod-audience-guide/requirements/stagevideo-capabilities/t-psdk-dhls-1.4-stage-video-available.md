---
description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo，TVSDK不會發出錯誤。 您的應用程式可藉由接聽StageVideoAvailabilityEvent來判斷StageVideo是否可用。
title: 檢查StageVideo是否可用
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo，TVSDK不會發出錯誤。 您的應用程式可藉由接聽StageVideoAvailabilityEvent來判斷StageVideo是否可用。

從Flash15和更新版本，當硬體時 `StageVideo` 無法使用，它將回覆至軟體 `StageVideo`. 若為Flash14及舊版，您可以判斷是否 `StageVideo` 可用。 若 `StageVideo` 無法使用，您可以使用 `StageVideoAvailabilityEvent` 以瞭解無法使用的原因。

1. 聆聽 `StageVideoAvailabilityEvent` 以判斷是否 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 若 `StageVideo` 無法使用，請核取 `flash.media.StageVideoAvailabilityReason`.
