---
description: 應用程式必須在適當的時間使用相應的TimedMetadata對象。
title: 在調度時儲存定時元資料對象
exl-id: db8b303a-441e-4cc0-a80d-dc9afda482b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 在調度時儲存定時元資料對象 {#store-timed-metadata-objects-as-they-are-dispatched}

應用程式必須在適當的時間使用相應的TimedMetadata對象。

在內容分析期間（在播放之前）,TVSDK識別訂閱的標籤並將這些標籤通知您的應用程式。 與每個關聯的時間 `TimedMetadata` 是播放時間線上的本地時間。

您的應用程式必須完成以下任務：

1. 跟蹤當前播放時間。
1. 將當前播放時間與已調度時間匹配 `TimedMetadata` 對象。

1. 使用 `TimedMetadata` 其中，開始時間等於當前本地播放時間。

   以下示例說明如何保存 `TimedMetadata` 對象 `ArrayList`。

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
