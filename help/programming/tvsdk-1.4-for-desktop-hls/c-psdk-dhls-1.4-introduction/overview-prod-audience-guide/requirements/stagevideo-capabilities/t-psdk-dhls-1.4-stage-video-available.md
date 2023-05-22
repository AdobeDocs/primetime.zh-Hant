---
description: 如果StageVideo不可用，且您的應用程式嘗試使用StageVideo，則TVSDK不會發出錯誤。 您的應用程式可以通過偵聽StageVideoAvailabilityEvent來確定StageVideo是否可用。
title: 檢查StageVideo是否可用
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，且您的應用程式嘗試使用StageVideo，則TVSDK不會發出錯誤。 您的應用程式可以通過偵聽StageVideoAvailabilityEvent來確定StageVideo是否可用。

從Flash15及更高版本，當硬體 `StageVideo` 不可用，它將回退到軟體 `StageVideo`。 對於Flash14和更早版本，您可以確定 `StageVideo` 的子菜單。 如果 `StageVideo` 不可用，您可以 `StageVideoAvailabilityEvent` 來理解為什麼它不可用。

1. 聽 `StageVideoAvailabilityEvent` 確定 `StageVideo` 的子菜單。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 不可用，檢查 `flash.media.StageVideoAvailabilityReason`。
