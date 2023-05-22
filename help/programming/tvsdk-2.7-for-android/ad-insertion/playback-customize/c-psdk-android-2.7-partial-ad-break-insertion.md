---
title: 部分廣告分段插入
description: 部分廣告分段插入
copied-description: true
exl-id: bcd4b108-9b91-479e-8147-ec4d24862e37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 部分廣告分段插入 {#partial-ad-break-insertion}

你可以像電視一樣體驗，能夠在廣告的中間，在直播中加入。 部分廣告中斷功能可以模擬類似電視的體驗，如果客戶端在某個微博內啟動一個即時流，它將在該微博內啟動。 類似電視頻道，廣告無縫

例如，如果用戶在90秒廣告中斷（3個30秒廣告）的中間加入，在第二個廣告中加入10秒（即，在廣告中斷開始40秒），則會發生以下情況：

* 第二廣告在剩餘持續時間（20秒）內被播放，隨後是第三廣告。
* 未觸發部分播放的廣告（第二個廣告）的廣告跟蹤器。 只觸發第三個廣告的跟蹤器。

預設情況下未啟用此行為。 要啟用此功能在應用中工作，請執行以下操作：

1. 使用AdvertingMetadata類的方法setEnableLivePreroll禁用即時預覽。

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 開啟「部分Ad-break插入」的首選項。 使用MediaPlayer介面中的新方法setPartialAdBreakPref將此功能開啟。 使用getPartialAdBreakPref方法查找此首選項的當前狀態。

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
