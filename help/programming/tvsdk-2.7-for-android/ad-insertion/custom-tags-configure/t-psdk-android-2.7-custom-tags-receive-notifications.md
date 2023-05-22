---
description: 要接收有關清單中標籤的通知，您需要實現相應的事件偵聽器。
title: 為定時元資料通知添加偵聽器
exl-id: e38f2a25-3379-4132-a8de-6703dc564ed4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 為定時元資料通知添加偵聽器 {#add-listeners-for-timed-metadata-notifications}

要接收有關清單中標籤的通知，您需要實現相應的事件偵聽器。

您可以通過偵聽 `onTimedMetadata`，它會將相關活動通知您的應用程式。 每次在分析內容期間標識唯一的預訂標籤時，TVSDK準備新的 `TimedMetadata` 對象並調度此事件。 對象包含您訂閱的標籤的名稱、此標籤將出現的回放中的本地時間以及其他資料。

1. 聽好事。

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

ID3元資料使用相同 `onTimedMetadata` 用於指示ID3標籤存在的偵聽器。 但是，這不應引起任何混亂，因為您可以使用 `TimedMetadata` `type` 用於區分TAG和ID3的屬性。 有關ID3標籤的詳細資訊，請參見  [ID3標籤](../../content-playback-options/t-psdk-android-2.7-id3-metadata-retrieve.md)。
