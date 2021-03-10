---
description: PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。
title: 使用MediaPlayer物件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---


# 使用MediaPlayer物件{#work-with-mediaplayer-objects}

PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。

## 關於MediaPlayerItem類{#section_B6F36C0462644F5C932C8AA2F6827071}

媒體資源成功載入後，TVSDK會建立`PTMediaPlayerItem`類別的例項，以提供該資源的存取權。

`PTMediaPlayer`會解析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 `PTMediaPlayerItem`實例是在資源解析後生成的，該實例是介質資源的已解析版本。 TVSDK可透過`PTMediaPlayer.currentItem`存取新建立的`PTMediaPlayerItem`例項。

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。

## MediaPlayer物件生命週期{#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

從您建立`PTMediaPlayer`例項到您終止（重複使用或移除）該例項的那一刻起，此例項將完成一系列從狀態切換到狀態的切換。

某些操作僅在播放器處於特定狀態時才允許。 例如，不允許在`PTMediaPlayerStatusCreated`中呼叫`play`。 您只有在播放器達到`PTMediaPlayerStatusReady`狀態後，才可呼叫此狀態。

要使用狀態：

* 您可以使用`PTMediaPlayer.status`擷取MediaPlayer物件的目前狀態。
* 狀態清單在`PTMediaPlayerStatus`中定義。

MediaPlayer實例生命週期的狀態轉換圖：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

下表提供其他詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>發生於</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式呼叫<span class="codeph"> playerWithMediaPlayerItem</span>以要求新的媒體播放器。 新建立的播放器正在等候您指定媒體播放器項目。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式會呼叫<span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>，媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>內容已準備好，廣告已插入時間軸，或廣告程式失敗。 可以開始緩衝或播放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫<span class="codeph"> play</span>，所以TVSDK正嘗試播放視訊。 視訊實際播放前可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態與<span class="codeph"> PTMediaPlayerStatusPlaying</span>之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>播放器到達串流結束，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，而媒體播放器也會發佈任何相關資源。 您無法再使用此例項 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>進程期間發生錯誤。 錯誤也可能會影響應用程式的下一步動作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關程式的意見回應（例如，在等待下一個狀態變更時使用微調按鈕），或在播放媒體時採取下一步驟，例如在呼叫下一個方法之前等待適當的狀態。