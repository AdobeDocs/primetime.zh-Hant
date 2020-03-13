---
description: PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。
seo-description: PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。
seo-title: 使用MediaPlayer物件
title: 使用MediaPlayer物件
uuid: 0c33ebd6-b11a-4e62-8c1c-880cfceff474
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 使用MediaPlayer物件 {#work-with-mediaplayer-objects}

PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。

## 關於MediaPlayerItem類 {#section_B6F36C0462644F5C932C8AA2F6827071}

媒體資源成功載入後，TVSDK會建立類別的例項， `PTMediaPlayerItem` 以提供該資源的存取權。

解 `PTMediaPlayer` 析媒體資源、載入相關資訊清單檔案，並解析資訊清單。 這是資源載入過程的非同步部分。 實 `PTMediaPlayerItem` 例是在資源解析後生成的，此實例是介質資源的解析版本。 TVSDK可讓您透過存取新建 `PTMediaPlayerItem` 的例項 `PTMediaPlayer.currentItem`。

>[!TIP]
>
>您必須等待資源成功載入，才能存取媒體播放器項目。

## MediaPlayer物件生命週期 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

從您建立執行個體 `PTMediaPlayer` 到終止（重複使用或移除）執行個體，此執行個體會完成一系列從一個狀態切換到另一個狀態的切換。

某些操作僅在播放器處於特定狀態時才允許。 例如，不允許 `play` 呼叫 `PTMediaPlayerStatusCreated` 中。 您只能在播放器達到狀態後才可呼叫此 `PTMediaPlayerStatusReady` 狀態。

要使用狀態：

* 您可以使用來檢索MediaPlayer對象的當前狀態 `PTMediaPlayer.status`。
* 狀態清單在中定義 `PTMediaPlayerStatus`。

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
   <td colname="col2"> <p>您的應用程式呼叫playerWithMediaPlayerItem，以要求新的媒 <span class="codeph"> 體播放器</span>。 新建立的播放器正在等候您指定媒體播放器項目。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>您的應用程 <span class="codeph"> 式會呼叫PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>，而媒體播放器正在載入。 </p> </td> 
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
   <td colname="col2"> <p>您的應用程式已 <span class="codeph"> 稱為play</span>，所以TVSDK正嘗試播放視訊。 視訊實際播放前可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態和 <span class="codeph"> PTMediaPlayerStatusPlaying之間移動</span>。 </p> </td> 
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