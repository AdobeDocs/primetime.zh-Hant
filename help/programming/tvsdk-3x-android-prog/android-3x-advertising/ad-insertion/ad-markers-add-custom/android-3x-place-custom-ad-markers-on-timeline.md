---
description: 此示例顯示了在播放時間線上包含自定義廣告標籤的推薦方法。
title: 在時間軸上放置自定義廣告標籤
exl-id: 32a4b342-1f26-42c5-9682-789c541f0fa6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 在時間軸上放置自定義廣告標籤 {#place-custom-ad-markers-on-the-timeline}

此示例顯示了在播放時間線上包含自定義廣告標籤的推薦方法。

1. 將帶外廣告定位資訊轉換為 `RepaceTimeRange` 類。
1. 建立實例 `CustomRangeMetadata` 類，並使用 `setTimeRangeList` 以list/array作為其參數來設定其時間範圍清單的方法。
1. 使用 `setType` 將類型設定為的方法 `MARK_RANGE`。
1. 使用 `MediaPlayerItemConfig.setCustomRangeMetadata` 方法 `CustomRangeMetadata` 實例，作為其參數來設定自定義範圍元資料。
1. 使用 `MediaPlayer.replaceCurrentResource` 方法 `MediaPlayerItemConfig` 實例作為其參數來設定，使新資源成為當前資源。
1. 等待 `STATE_CHANGED` 事件，它報告玩家在 `PREPARED` 狀態。
1. 通過呼叫啟動視頻播放 `MediaPlayer.play`。

下面是完成本示例中任務的結果：

* 如果 `ReplaceTimeRange` 與回放時間軸上的另一個重疊，例如， `ReplaceTimeRange` 早於已放置的結束位置，TVSDK會靜默地調整違規的開始 `ReplaceTimeRange` 避免衝突。

   這樣， `ReplaceTimeRange` 比最初指定的短。 如果調整導致持續時間為零，則TVSDK會以靜默方式刪除違規 `ReplaceTimeRange`。

* TVSDK為自定義廣告分段查找相鄰時間範圍，並將它們分成單獨的廣告分段。

不與任何其他時間範圍相鄰的時間範圍被轉換為包含單個廣告的廣告分段。

* 如果應用程式嘗試載入其配置包含 `CustomRangeMetadata` TVSDK只能用於上下文自定義廣告標籤，如果基礎資產不是VOD類型，則會引發異常。

* 在處理自定義廣告標籤時，TVSDK會停用其他廣告解析機制(例如，Adobe Primetime廣告決定)。

   可以使用任何TVSDK ad-resolver模組或自定義ad標籤器機制。 使用自定義廣告標籤時，廣告內容會被視為已解析並放置在時間軸上。

以下代碼段將三個時間範圍作為自定義標籤放置在時間軸上。

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
