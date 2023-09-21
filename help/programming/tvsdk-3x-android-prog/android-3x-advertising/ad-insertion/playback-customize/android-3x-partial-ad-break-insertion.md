---
title: 部分廣告插播插入
description: 部分廣告插播插入
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 部分廣告插播插入 {#partial-ad-break-insertion}

您可以啟用類似電視的體驗，即能夠在廣告中間、在直播串流中加入。 部分廣告插播功能可讓您模擬類似電視的體驗，如果使用者端在中間版本內開始即時資料流，則會從該中間版本內開始。 這類似於切換到電視頻道，廣告也順暢地執行。

例如，如果使用者在90秒的廣告插播（三個30秒的廣告）中加入，則在第二個廣告中加入10秒（即在廣告插播中加入40秒），就會發生以下情況：

* 第二個廣告會播放剩餘的持續時間（20秒），然後是第三個廣告。
* 部分播放的廣告（第二個廣告）的廣告追蹤器不會觸發。 僅觸發第三個廣告的追蹤器。

預設不會啟用此行為。 若要在應用程式中啟用此功能，請執行下列動作：

開啟「部分廣告插播插入」的偏好設定。 使用新方法 `setPartialAdBreakPref` 在MediaPlayer介面中開啟此功能。 使用 `getPartialAdBreakPref` 尋找此偏好設定目前狀態的方法。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

會播放前段廣告（如果有的話），然後從即時點播放內容，模擬直播電視的體驗。
