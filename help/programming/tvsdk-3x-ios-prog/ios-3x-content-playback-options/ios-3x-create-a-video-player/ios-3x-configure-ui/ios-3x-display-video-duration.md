---
description: 您可以顯示當前活動內容的持續時間。
title: 顯示視頻的持續時間
exl-id: a41cb291-9355-44cf-80bb-9c3cf6628b81
source-git-commit: 85818281390b68522da2663496be025acf8f8675
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# 顯示視頻的持續時間 {#display-the-duration-of-the-video}

您可以顯示當前活動內容的持續時間。

使用以下示例代碼實現視頻持續時間顯示：

的 `PTMediaPlayer` 屬性 [可瀏覽範圍](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)，包含當前可查看的窗口範圍：

* 對於視頻點播，這個範圍是整個視頻點播內容範圍，包括廣告。
* 對於即時/線性，此範圍表示可查看的窗口。

有關API的詳細資訊，請參見 [TVSDK 3.4 foriOSAPI參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
