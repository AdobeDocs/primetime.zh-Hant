---
description: 'null'
seo-description: 'null'
seo-title: 插入部分廣告分段
title: 插入部分廣告分段
uuid: a81295b8-77fe-4475-a472-080ee7804d7a
translation-type: tm+mt
source-git-commit: fe9d7d1b2b23a70eb4e212de3d9bda47fc11d8f1

---


# 部分插入廣告插入 {#partial-ad-break-insertion}

您可以啟用類似電視的體驗，讓您能夠在廣告中間加入即時串流。 「部分廣告」中斷功能可讓您模擬類似電視的體驗，如果用戶端在midroll中啟動即時串流，則會在該midroll中啟動。 它類似於切換電視頻道，廣告也順暢運作。

例如，如果使用者在90秒廣告插播（3個30秒廣告）的中間加入，在第二個廣告中加入10秒（亦即，在廣告插播中加入40秒），則會發生下列情況：

* 第二個廣告會在剩餘的持續時間（20秒）內播放，接著是第三個廣告。
* 部分播放廣告（第二個廣告）的廣告追蹤器不會引發。 只會引發第三個廣告的追蹤器。

預設情況下不啟用此行為。 若要在您的應用程式中啟用此功能，請執行下列動作：

開啟「部分插入廣告插入」偏好設定。 使用MediaPlayer介面中 `setPartialAdBreakPref` 的新方法，將此功能開啟。 使用 `getPartialAdBreakPref` 方法可找到此首選項的當前狀態。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

播放前段廣告（如果有的話），然後內容從即時點播放，以模擬即時電視的體驗。
