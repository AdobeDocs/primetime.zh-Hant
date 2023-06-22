---
description: 從您建立MediaPlayer例項的那一刻到您終止（重複使用或移除）該例項的那一刻，此例項會完成狀態之間的一系列轉換。
title: MediaPlayer物件生命週期
exl-id: efb39fea-1050-41e5-93d8-1175a54f81e5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# MediaPlayer物件生命週期{#mediaplayer-object-lifecycle}

從您建立MediaPlayer例項的那一刻到您終止（重複使用或移除）該例項的那一刻，此例項會完成狀態之間的一系列轉換。

只有播放器處於特定狀態時，才允許進行某些操作。 例如，呼叫 `play` 在 `IDLE` 不允許。 只有在播放器到達 `PREPARED` 州別。

若要使用狀態：

* 您可以擷取 `MediaPlayer` 物件與 `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* 狀態清單定義於 `MediaPlayer.PlayerState`.

生命週期的狀態轉換圖 `MediaPlayer` 例項：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

下表提供其他詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 閒置 </span> </td> 
   <td colname="col2"> <p>您的應用程式呼叫來要求新的媒體播放器 <span class="codeph"> DefaultMediaPlayer.create </span>. 新建立的播放器正等待您指定媒體播放器專案。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在初始化 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> MediaPlayer.replaceCurrentItem </span>，且媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化 </span> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在準備 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> MediaPlayer.prepareToPlay </span>. 媒體播放器正在載入媒體播放器專案和相關資源。 </p> <p>提示：可能會發生主要媒體的某些緩衝。 </p> <p>TVSDK正在準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 </p> <p>提示：若要將開始時間設定為非零值，請呼叫 <span class="codeph"> prepareToPlay(startTime) </span> 以毫秒為單位的時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已準備 </span> </td> 
   <td colname="col2"> <p>內容已準備好，且廣告已插入時間軸中，或廣告程式失敗。 緩衝或播放可以開始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在播放 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> play </span>，因此TVSDK正嘗試播放視訊。 某些緩衝可能會發生在視訊實際播放之前。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停 </span> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態和「正在播放」之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停 </span> </td> 
   <td colname="col2"> <p>您的應用程式在播放器播放或暫停時離開播放、關閉裝置或切換應用程式。 媒體播放器已暫停，資源已釋放。 若要繼續，請還原媒體播放器。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 完成 </span> </td> 
   <td colname="col2"> <p>播放器到達串流結尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已發行 </span> </td> 
   <td colname="col2"> <p>您的應用程式已發行媒體播放器，也會發行任何相關資源。 您無法再使用此執行個體 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 錯誤 </span> </td> 
   <td colname="col2"> <p>處理期間發生錯誤。 錯誤也可能會影響您的應用程式接下來可以執行的動作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供程式的意見回饋（例如，在等待下一個狀態變更時執行旋轉圖示），或是在播放媒體時執行下一個步驟，例如在呼叫下一個方法之前等待適當的狀態。

例如：

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```
