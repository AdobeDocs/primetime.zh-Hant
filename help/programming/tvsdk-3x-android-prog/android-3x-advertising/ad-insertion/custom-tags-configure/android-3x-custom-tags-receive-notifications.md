---
description: 若要接收資訊清單中標籤的通知，您必須實作適當的事件接聽程式。
seo-description: 若要接收資訊清單中標籤的通知，您必須實作適當的事件接聽程式。
seo-title: 新增計時中繼資料通知的監聽器
title: 新增計時中繼資料通知的監聽器
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 新增計時中繼資料通知的監聽器 {#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的通知，您必須實作適當的事件接聽程式。

您可以監聽計時的中繼資料，以 `onTimedMetadata`通知您的應用程式相關活動。 每次在剖析內容時識別唯一的訂閱標籤時，TVSDK會準備新物件並 `TimedMetadata` 分派此事件。 物件包含您所訂閱之標籤的名稱、此標籤將出現的播放中的本機時間，以及其他資料。

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

ID3中繼資料使用相 `onTimedMetadata` 同的監聽器來指出ID3標籤的存在。 不過，這不會造成任何混淆，因為您可以使 `TimedMetadata` 用屬 `type` 性來區分TAG和ID3。 如需ID3標籤的詳細資訊，請參 [閱ID3標籤](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md)。