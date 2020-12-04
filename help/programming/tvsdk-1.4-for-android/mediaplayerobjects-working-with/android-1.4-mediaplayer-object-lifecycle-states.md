---
description: 從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。
seo-description: 從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。
seo-title: MediaPlayer物件生命週期
title: MediaPlayer物件生命週期
uuid: 6670a30c-7053-4754-bc36-6bb8590c001d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# MediaPlayer物件生命週期{#mediaplayer-object-lifecycle}

從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。

某些操作僅在播放器處於特定狀態時才允許。 例如，不允許在`IDLE`中呼叫`play`。 您只有在播放器達到`PREPARED`狀態後，才可呼叫此狀態。

要使用狀態：

* 可以使用`MediaPlayer.getStatus`檢索`MediaPlayer`對象的當前狀態。

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* 狀態清單在`MediaPlayer.PlayerState`中定義。

`MediaPlayer`實例生命週期的狀態轉移圖：
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
   <td colname="col1"> <span class="codeph"> 空閒  </span> </td> 
   <td colname="col2"> <p>您的應用程式呼叫<span class="codeph"> DefaultMediaPlayer.create </span>來要求新的媒體播放器。 新建立的播放器正在等候您指定媒體播放器項目。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 初始化  </span> </td> 
   <td colname="col2"> <p>您的應用程式名為<span class="codeph"> MediaPlayer.replaceCurrentItem </span>，媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化  </span> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 準備  </span> </td> 
   <td colname="col2"> <p>您的應用程式名為<span class="codeph"> MediaPlayer.prepareToPlay </span>。 媒體播放器正在載入媒體播放器項目和相關資源。 </p> <p>提示： 可能會發生主媒體的緩衝。 </p> <p>TVSDK正在準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 </p> <p>提示： 若要將開始時間設為非零值，請呼叫<span class="codeph"> prepareToPlay(startTime)</span>，以毫秒為單位。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 準備好  </span> </td> 
   <td colname="col2"> <p>內容已準備好，廣告已插入時間軸，或廣告程式失敗。 可以開始緩衝或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 播放  </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫<span class="codeph"> play </span>，所以TVSDK正嘗試播放視訊。 視訊實際播放前可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 暫停  </span> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態和播放之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停  </span> </td> 
   <td colname="col2"> <p>您的應用程式在播放或暫停播放時已導覽離開播放、關閉裝置或已切換應用程式。 媒體播放器已暫停，資源已釋放。 要繼續，請恢復媒體播放器。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 完成  </span> </td> 
   <td colname="col2"> <p>播放器到達串流結束，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已發佈  </span> </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，而媒體播放器也會發佈任何相關資源。 您無法再使用此例項 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 錯誤  </span> </td> 
   <td colname="col2"> <p>進程期間發生錯誤。 錯誤也可能會影響應用程式的下一步動作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關程式的回饋（例如，在等待下一個狀態變更時使用微調按鈕），或在播放媒體時採取下一步驟，例如在呼叫下一個方法之前等待適當的狀態。

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

