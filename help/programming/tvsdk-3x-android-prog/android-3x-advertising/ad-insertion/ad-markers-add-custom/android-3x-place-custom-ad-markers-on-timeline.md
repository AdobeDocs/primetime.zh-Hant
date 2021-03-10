---
description: 此範例顯示在播放時間軸上包含自訂廣告標籤的建議方式。
title: 在時間軸上放置自訂廣告標籤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# 將自訂廣告標籤置於時間軸{#place-custom-ad-markers-on-the-timeline}

此範例顯示在播放時間軸上包含自訂廣告標籤的建議方式。

1. 將帶外廣告定位資訊轉換為`RepaceTimeRange`類的清單／陣列。
1. 建立`CustomRangeMetadata`類的實例，並將其`setTimeRangeList`方法與list/array一起使用作為其參數來設定其時間範圍清單。
1. 使用其`setType`方法將類型設定為`MARK_RANGE`。
1. 使用`MediaPlayerItemConfig.setCustomRangeMetadata`方法及`CustomRangeMetadata`例項作為其引數來設定自訂範圍中繼資料。
1. 使用`MediaPlayer.replaceCurrentResource`方法和`MediaPlayerItemConfig`實例作為其參數，設定使新資源成為當前資源。
1. 等待`STATE_CHANGED`事件，該事件會報告播放器處於`PREPARED`狀態。
1. 呼叫`MediaPlayer.play`以開始視訊播放。

以下是完成此示例中任務的結果：

* 例如，如果`ReplaceTimeRange`與播放時間軸上的另一個重疊，則`ReplaceTimeRange`的開始位置早於已放置的結束位置，TVSDK會無訊息地調整違規`ReplaceTimeRange`的開始位置，以避免衝突。

   這會使調整後的`ReplaceTimeRange`比原本指定的短。 如果調整導致持續時間為零，TVSDK會以無訊息的方式捨棄違規的`ReplaceTimeRange`。

* TVSDK會尋找自訂廣告插播的鄰近時間範圍，並將它們叢集為個別廣告插播。

與任何其他時間範圍不相鄰的時間範圍會轉換為包含單一廣告的廣告分段。

* 如果應用程式嘗試載入其設定包含`CustomRangeMetadata`的媒體資源，而該媒體資源僅能用於內容自訂廣告標籤，則TVSDK會在基礎資產不是VOD類型時引發例外。

* 處理自訂廣告標籤時，TVSDK會停用其他廣告解析機制(例如，Adobe Primetime廣告決策)。

   您可以使用任何TVSDK廣告解析程式模組或自訂廣告標籤機制。 當您使用自訂廣告標籤時，廣告內容會被視為已解析，並置於時間軸上。

下列程式碼片段會將三個時間範圍放置在時間軸上做為自訂廣告標籤。

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
