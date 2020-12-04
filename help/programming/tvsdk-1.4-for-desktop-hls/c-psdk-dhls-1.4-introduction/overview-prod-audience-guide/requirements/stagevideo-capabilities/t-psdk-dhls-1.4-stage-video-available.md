---
description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。
seo-description: 如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。
seo-title: 檢查StageVideo是否可用
title: 檢查StageVideo是否可用
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# 檢查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo無法使用，而您的應用程式嘗試使用StageVideo,TVSDK不會發出錯誤。 您的應用程式可以監聽StageVideoAvailabilityEvent，以判斷StageVideo是否可用。

在Flash 15和更新版本中，當硬體`StageVideo`不可用時，它會回到軟體`StageVideo`。 對於Flash 14及舊版軟體，您可決定是否提供`StageVideo`。 如果`StageVideo`不可用，您可以使用`StageVideoAvailabilityEvent`瞭解它不可用的原因。

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
