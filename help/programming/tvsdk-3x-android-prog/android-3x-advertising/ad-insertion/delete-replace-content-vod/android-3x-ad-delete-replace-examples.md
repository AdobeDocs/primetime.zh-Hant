---
description: 以下是刪除和取代廣告的程式範例。
seo-description: 以下是刪除和取代廣告的程式範例。
seo-title: 刪除和取代廣告的範例
title: 刪除和取代廣告的範例
uuid: 6bf9d71a-73fe-4033-b97a-6b0cff8687f2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 刪除和取代廣告的範例 {#examples-to-delete-and-replace-ads}

以下是刪除和取代廣告的程式範例。

以下是使用的範例 `DELETE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means,  
// like a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, o)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.DELETE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource  
mediaPlayer.replaceCurrentResource(mediaResource, config);
```

以下是使用的範例 `REPLACE_RANGE`:

```java
// Assume that the 3 timerange specs are obtained through external means, like 
//  a CMS. Assume mediaPlayer is an instance of a properly configured MediaPlayer 
// Use these 3 timerange specs to populate the RepaceTimeRange list 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 10000)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 20000)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 30000)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.REPLACE_RANGE); 
 
// create a MediaResource instance 
MediaResource mediaResource = ... ; 
 
// create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config = new MediaPlayerItemConfig(getActivity() 
    .getApplicationContext()); 
 
// Set Auditude settings, which are used for ad replacement, for this  
//  MediaPlayerItemConfig instance, 
 
... 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// prepare the content for playback by calling replaceCurrentResource 
mediaPlayer.replaceCurrentResource(mediaResource, config);
```
