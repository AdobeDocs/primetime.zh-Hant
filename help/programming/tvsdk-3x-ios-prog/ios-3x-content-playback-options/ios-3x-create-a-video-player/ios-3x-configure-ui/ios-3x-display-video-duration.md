---
description: 您可以顯示目前作用中內容的持續時間。
seo-description: 您可以顯示目前作用中內容的持續時間。
seo-title: 顯示視訊的持續時間
title: 顯示視訊的持續時間
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# 顯示視訊的持續時間 {#display-the-duration-of-the-video}

您可以顯示目前作用中內容的持續時間。

使用下列范常式式碼實作視訊持續時間顯示：

    「PTMediaPlayer」屬性「[seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)」包含目前可檢視的視窗範圍：
    
    *對於VOD，此範圍是整個VOD內容範圍，包括廣告。
    *對於即時／線性，此範圍代表可檢視的視窗。
    
    如需API的詳細資訊，請參閱[TVSDK 3.4 for iOS API參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
