---
title: 部分廣告分段插入
description: 部分廣告分段插入
copied-description: true
exl-id: c86f1e99-7f1e-4a1e-b285-568ad6659f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 部分Ad-break插入 {#partial-ad-break-insertion}

你可以像電視一樣體驗，能夠在廣告的中間，在直播中加入。 部分廣告中斷功能可以模擬類似電視的體驗，如果客戶端在某個微博內啟動一個即時流，它將在該微博內啟動。 類似電視頻道，廣告無縫

例如，如果用戶在90秒廣告中斷（3個30秒廣告）的中間加入，在第二個廣告中加入10秒（即，在廣告中斷開始40秒），則會發生以下情況：

* 第二廣告在剩餘持續時間（20秒）內被播放，隨後是第三廣告。
* 未觸發部分播放的廣告（第二個廣告）的廣告跟蹤器。 只觸發第三個廣告的跟蹤器。

預設情況下未啟用此行為。 要啟用此功能在應用中工作，請執行以下操作：

開啟「部分Ad-break插入」的首選項。 使用新方法 `setPartialAdBreakPref` 在MediaPlayer介面中，將此功能開啟。 使用 `getPartialAdBreakPref` 方法來查找此首選項的當前狀態。

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

如果可用，播放預播廣告，然後內容從實況點播放，模擬實況電視的體驗。
