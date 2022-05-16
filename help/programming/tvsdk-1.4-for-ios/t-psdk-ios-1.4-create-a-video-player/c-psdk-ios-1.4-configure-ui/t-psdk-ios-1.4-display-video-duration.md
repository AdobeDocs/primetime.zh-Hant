---
description: 您可以顯示當前活動內容的持續時間。
title: 顯示視頻的持續時間
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 顯示視頻的持續時間 {#display-the-duration-of-the-video}

您可以顯示當前活動內容的持續時間。

使用以下示例代碼實現視頻持續時間顯示：

的 `PTMediaPlayer` 屬性 [可瀏覽範圍](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)，包含當前可查看的窗口範圍：

* 對於視頻點播，這個範圍是整個視頻點播內容範圍，包括廣告。
* 對於即時/線性，此範圍表示可查看的窗口。

有關API的詳細資訊，請參見 [TVSDK 1.4 foriOSAPI參考](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
