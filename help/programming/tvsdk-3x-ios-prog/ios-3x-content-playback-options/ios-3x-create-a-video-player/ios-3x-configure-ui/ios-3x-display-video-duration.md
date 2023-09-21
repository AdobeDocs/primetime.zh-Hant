---
description: 您可以顯示目前作用中內容的持續時間。
title: 顯示視訊的持續時間
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 顯示視訊的持續時間 {#display-the-duration-of-the-video}

您可以顯示目前作用中內容的持續時間。

使用下列範常式式碼實作視訊持續時間顯示：

此 `PTMediaPlayer` 屬性， [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)，包含目前可搜尋的視窗範圍：

* 對於VOD，此範圍是整個VOD內容範圍，包括廣告。
* 若為即時/線性，此範圍代表可搜尋視窗。

如需有關API的詳細資訊，請參閱 [iOS API適用的TVSDK 3.4參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
