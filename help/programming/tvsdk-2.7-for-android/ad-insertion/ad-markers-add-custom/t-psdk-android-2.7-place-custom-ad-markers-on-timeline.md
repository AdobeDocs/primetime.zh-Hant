---
description: 此範例說明在播放時間軸上加入自訂廣告標籤的建議方法。
title: 在時間軸上放置自訂廣告標籤
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 在時間軸上放置自訂廣告標籤 {#place-custom-ad-markers-on-the-timeline}

此範例說明在播放時間軸上加入自訂廣告標籤的建議方法。

1. 將頻外廣告定位資訊轉換為清單/陣列 `RepaceTimeRange` 類別。
1. 建立例項 `CustomRangeMetadata` 類別，並使用其 `setTimeRangeList` 以list/array作為其引數以設定其時間範圍清單的方法。
1. 使用其 `setType` 設定型別的方法 `MARK_RANGE`.
1. 使用 `MediaPlayerItemConfig.setCustomRangeMetadata` 具有的方法 `CustomRangeMetadata` 執行個體作為引數，以設定自訂範圍中繼資料。
1. 使用 `MediaPlayer.replaceCurrentResource` 具有的方法 `MediaPlayerItemConfig` 執行個體作為引數，以設定讓新資源成為目前資源。
1. 等待 `STATE_CHANGED` 事件，報告播放器是否在 `PREPARED` 州別。
1. 透過呼叫開始播放視訊 `MediaPlayer.play`.

以下是完成此範例中工作的結果： >
* 如果 `ReplaceTimeRange` 與播放時間軸上的另一個專案重疊，例如， `ReplaceTimeRange` 早於已放置的結束位置，TVSDK會以無訊息方式調整違規的開頭 `ReplaceTimeRange` 以避免衝突。

  如此一來，調整後的 `ReplaceTimeRange` 比最初指定的短。 如果調整導致持續時間為零，TVSDK會以無訊息方式捨棄違規專案 `ReplaceTimeRange`.

* TVSDK會尋找自訂廣告插播的相鄰時間範圍，並將其叢集為個別的廣告插播。

  與任何其他時間範圍不相鄰的時間範圍會轉換為包含單一廣告的廣告插播。
* 如果應用程式嘗試載入的媒體資源組態包含 `CustomRangeMetadata` 如果基礎資產不是VOD型別，則TVSDK會擲回例外狀況。
* 處理自訂廣告標籤時，TVSDK會停用其他廣告解析機制(例如Adobe Primetime ad decisioning)。

  您可以使用任何TVSDK廣告解析程式模組或自訂廣告標籤機制。 當您使用自訂廣告標籤時，廣告內容會被視為已解析並放置在時間軸上。

下列程式碼片段會在時間軸上放置三個時間範圍，做為自訂廣告標籤。

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
