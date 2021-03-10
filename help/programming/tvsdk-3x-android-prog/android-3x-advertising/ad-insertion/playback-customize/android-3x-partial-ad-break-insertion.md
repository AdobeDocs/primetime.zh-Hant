---
title: 插入部分廣告分段
description: 插入部分廣告分段
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# 部分插入廣告插入{#partial-ad-break-insertion}

您可以啟用類似電視的體驗，讓您能夠在廣告中間加入即時串流。 「部分廣告」中斷功能可讓您模擬類似電視的體驗，如果用戶端在midroll中啟動即時串流，則會在該midroll中啟動。 它類似於切換電視頻道，廣告也順暢運作。

例如，如果使用者在90秒廣告插播（3個30秒廣告）的中間加入，在第二個廣告中加入10秒（亦即，在廣告插播中加入40秒），則會發生下列情況：

* 第二個廣告會在剩餘的持續時間（20秒）內播放，接著是第三個廣告。
* 部分播放廣告（第二個廣告）的廣告追蹤器不會引發。 只會引發第三個廣告的追蹤器。

預設情況下不啟用此行為。 若要在您的應用程式中啟用此功能，請執行下列動作：

開啟「部分插入廣告插入」偏好設定。 使用MediaPlayer介面中的新方法`setPartialAdBreakPref`來開啟此功能。 使用`getPartialAdBreakPref`方法查找此首選項的當前狀態。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

播放前段廣告（如果有的話），然後內容從即時點播放，以模擬即時電視的體驗。
