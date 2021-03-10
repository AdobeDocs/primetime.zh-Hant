---
description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。
title: 檢查StageVideo是否可用
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。

從Flash15和更高版本開始，當硬體`StageVideo`不可用時，它將返回軟體`StageVideo`。 對於Flash14和舊版，您可以確定`StageVideo`是否可用。 如果`StageVideo`不可用，您可以使用`StageVideoAvailabilityEvent`瞭解它不可用的原因。

1. 監聽`StageVideoAvailabilityEvent`以確定`StageVideo`是否可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果`StageVideo`不可用，請檢查`flash.media.StageVideoAvailabilityReason`。
