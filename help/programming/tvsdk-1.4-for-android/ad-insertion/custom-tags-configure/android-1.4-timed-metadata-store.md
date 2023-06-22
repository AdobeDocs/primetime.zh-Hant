---
description: 您的應用程式必須在適當的時間使用適當的TimedMetadata物件。
title: 在傳送定時中繼資料物件時將其儲存
exl-id: db8b303a-441e-4cc0-a80d-dc9afda482b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 在傳送定時中繼資料物件時將其儲存 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用適當的TimedMetadata物件。

在內容剖析期間（發生在播放之前），TVSDK會識別訂閱的標籤，並通知您的應用程式這些標籤。 與每個報表套裝相關聯的時間 `TimedMetadata` 是播放時間軸上的當地時間。

您的應用程式必須完成下列工作：

1. 追蹤目前的播放時間。
1. 比對目前播放時間與已傳送的時間 `TimedMetadata` 物件。

1. 使用 `TimedMetadata` 其中開始時間等於目前的本機播放時間。

   以下範例說明如何儲存 `TimedMetadata` 中的物件 `ArrayList`.

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
