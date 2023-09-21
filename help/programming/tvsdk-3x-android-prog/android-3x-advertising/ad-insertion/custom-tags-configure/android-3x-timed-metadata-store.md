---
description: 您的應用程式必須在適當的時間使用適當的TimedMetadata物件。
title: 在傳送定時中繼資料物件時將其儲存
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# 在傳送定時中繼資料物件時將其儲存 {#store-timed-metadata-objects-as-they-are-dispatched}

您的應用程式必須在適當的時間使用適當的TimedMetadata物件。

在播放前進行的內容剖析期間，TVSDK會識別訂閱的標籤，並通知您的應用程式這些標籤。

>[!TIP]
>
>與每個報表套裝相關聯的時間 `TimedMetadata` 是播放時間軸的當地時間。

若要在傳送定時中繼資料物件時儲存這些物件：

1. 追蹤目前的播放時間。
1. 比對目前的播放時間與已傳送的時間 `TimedMetadata` 物件。

1. 使用 `TimedMetadata` 其中開始時間等於目前的本機播放時間。

   下列範例顯示如何儲存 `TimedMetadata` 中的物件 `ArrayList`.

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
