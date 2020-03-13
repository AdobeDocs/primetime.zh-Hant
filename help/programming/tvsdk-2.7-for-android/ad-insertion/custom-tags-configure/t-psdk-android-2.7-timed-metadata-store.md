---
description: 您的應用程式必須在適當的時間使用適當的TimedMetadata物件。
seo-description: 您的應用程式必須在適當的時間使用適當的TimedMetadata物件。
seo-title: 傳送計時中繼資料物件時，可儲存這些物件
title: 傳送計時中繼資料物件時，可儲存這些物件
uuid: 0d0ddfea-6f32-467d-91bc-f18ceadcd842
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 傳送計時中繼資料物件時，可儲存這些物件 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用適當的TimedMetadata物件。

在內容剖析期間（在播放之前）,TVSDK會識別已訂閱的標籤，並通知您的應用程式這些標籤。

>[!TIP]
>
>與每個時間關聯的時 `TimedMetadata` 間是播放時間軸上的本地時間。

要在調度時儲存計時元資料對象，請執行以下操作：

1. 追蹤目前的播放時間。
1. 將當前播放時間與調度的對象匹 `TimedMetadata` 配。

1. 使用開 `TimedMetadata` 始時間等於目前本機播放時間的位置。

   以下示例說明如何在中 `TimedMetadata` 保存對象 `ArrayList`。

   ```java
   private List<TimedMetadata> _timedMetadataList =  
     new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

