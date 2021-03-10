---
description: 若要接收資訊清單中標籤的通知，您必須實作適當的事件接聽程式。
title: 新增計時中繼資料通知的監聽器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# 為計時中繼資料通知新增監聽器{#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，您必須實作適當的事件接聽程式。

您可以監聽`onTimedMetadata`來監視計時中繼資料，該監聽會通知您的應用程式相關活動。 每次在剖析內容時識別唯一的訂閱標籤時，TVSDK會準備新的`TimedMetadata`物件並分派此事件。 物件包含您所訂閱之標籤的名稱、此標籤將出現的播放中的本機時間，以及其他資料。

聽聽活動。

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

ID3中繼資料使用相同的`onTimedMetadata`監聽器來指示ID3標籤的存在。 但是，這不會造成任何混淆，因為您可以使用`TimedMetadata` `type`屬性來區分TAG和ID3。 如需ID3標籤的詳細資訊，請參閱[ID3標籤](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md)。