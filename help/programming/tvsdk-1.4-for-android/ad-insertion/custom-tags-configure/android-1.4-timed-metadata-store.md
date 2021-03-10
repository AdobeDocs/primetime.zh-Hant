---
description: 您的應用程式必須在適當的時間使用適當的TimedMetadata物件。
title: 傳送計時中繼資料物件時，可儲存這些物件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 將計時的中繼資料物件傳送至{#store-timed-metadata-objects-as-they-are-dispatched}時儲存

您的應用程式必須在適當的時間使用適當的TimedMetadata物件。

在內容剖析期間（在播放之前）,TVSDK會識別已訂閱的標籤，並通知您的應用程式這些標籤。 與每個`TimedMetadata`相關聯的時間是播放時間軸上的本地時間。

您的應用程式必須完成下列工作：

1. 追蹤目前的播放時間。
1. 將當前播放時間與已調度的`TimedMetadata`對象匹配。

1. 使用`TimedMetadata`，其中開始時間等於目前的本機播放時間。

   以下示例說明如何在`ArrayList`中保存`TimedMetadata`對象。

   ```java
   private List<TimedMetadata> _timedMetadataList = new ArrayList<TimedMetadata>(); 
   ... 
   public void onTimedMetadata(TimedMetadata timedMetadata) { 
       ... 
       if (timedMetadata.getName().equalsIgnoreCase("#EXT-X-CUE"))  { 
           _timedMetadataList.add(timedMetadata); 
       } 
       ... 
   }
   ```

