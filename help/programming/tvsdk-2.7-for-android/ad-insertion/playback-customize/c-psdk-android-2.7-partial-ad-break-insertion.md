---
title: 部分廣告插播插入
description: 部分廣告插播插入
copied-description: true
exl-id: bcd4b108-9b91-479e-8147-ec4d24862e37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 部分廣告插播插入 {#partial-ad-break-insertion}

您可以啟用類似電視的體驗，即能夠在廣告中間、在直播串流中加入。 部分廣告插播功能可讓您模擬類似電視的體驗，如果客戶在中間版本內開始即時資料流，它會從該中間版本內開始。 這類似於切換至電視頻道，而商業廣告則順暢運作。

例如，如果使用者在90秒的廣告插播（3個30秒的廣告）中間、第二個廣告的10秒（亦即廣告插播的40秒）中加入，會發生下列情況：

* 第二個廣告會播放剩餘的持續時間（20秒），然後是第三個廣告。
* 部分播放的廣告（第二個廣告）的廣告追蹤器不會觸發。 僅觸發第三個廣告的追蹤器。

預設不會啟用此行為。 若要在應用程式中啟用此功能，請執行以下操作：

1. 使用AdvertisingMetadata類別的方法setEnableLivePrerroll停用即時預列。

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. 開啟「部分廣告插播插入」的偏好設定。 使用MediaPlayer介面中的新方法setPartialAdBreakPref，將此功能切換為ON。 使用getPartialAdBreakPref方法尋找此偏好設定的目前狀態。

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
