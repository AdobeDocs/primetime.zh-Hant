---
description: 若要接收資訊清單中標籤的相關通知，您必須實作適當的事件接聽程式。
title: 為定時中繼資料通知新增接聽程式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 為定時中繼資料通知新增接聽程式 {#add-listeners-for-timed-metadata-notifications}

若要接收資訊清單中標籤的相關通知，您必須實作適當的事件接聽程式。

您可以透過聆聽來監視定時中繼資料 `onTimedMetadata`，會通知您應用程式相關活動。 每次在剖析內容期間識別出不重複的訂閱標籤時，TVSDK都會準備新的 `TimedMetadata` 物件並傳送此事件。 物件包含您訂閱的標簽名稱、此標籤出現所在的播放本地時間以及其他資料。

接聽事件。

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

ID3中繼資料使用相同的 `onTimedMetadata` 接聽程式來指示是否存在ID3標籤。 不過，這應該不會造成任何混淆，因為您可以使用 `TimedMetadata` `type` 屬性以區分TAG和ID3。 如需ID3標籤的詳細資訊，請參閱 [ID3標籤](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).
