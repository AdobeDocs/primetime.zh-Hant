---
description: PTMediaPlayer對象表示媒體播放器。 PTMediaPlayerItem表示播放器上的音頻或視頻。
title: 使用MediaPlayer對象
exl-id: 57dd455e-e78c-4e5b-80af-070ae7982864
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 使用MediaPlayer對象 {#work-with-mediaplayer-objects}

PTMediaPlayer對象表示媒體播放器。 PTMediaPlayerItem表示播放器上的音頻或視頻。

## 關於MediaPlayerItem類 {#section_B6F36C0462644F5C932C8AA2F6827071}

成功載入媒體資源後，TVSDK將建立 `PTMediaPlayerItem` 類以提供對該資源的訪問。

的 `PTMediaPlayer` 解析媒體資源，載入關聯的清單檔案，並解析清單。 這是資源載入進程的非同步部分。 的 `PTMediaPlayerItem` 實例在資源解析後生成，並且此實例是媒體資源的解析版本。 TVSDK提供對新建立的 `PTMediaPlayerItem` 實例 `PTMediaPlayer.currentItem`。

>[!TIP]
>
>必須等待資源成功載入後才能訪問媒體播放器項目。

## MediaPlayer對象生命週期 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

從您建立 `PTMediaPlayer` 實例到終止（重用或刪除）時，此實例將完成從一個狀態到另一個狀態的一系列過渡。

僅當播放器處於特定狀態時才允許某些操作。 例如，調用 `play` 在 `PTMediaPlayerStatusCreated` 不允許。 只有在玩家達到以下條件後，才可調用此狀態 `PTMediaPlayerStatusReady` 狀態。

要使用狀態，請執行以下操作：

* 可以使用檢索MediaPlayer對象的當前狀態 `PTMediaPlayer.status`。
* 狀態清單在中定義 `PTMediaPlayerStatus`。

MediaPlayer實例生命週期的狀態轉換圖：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

下表提供了更多詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>在</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式通過調用請求了新媒體播放器 <span class="codeph"> 播放器WithMediaPlayerItem</span>。 新建立的播放器正在等待您指定媒體播放器項。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式調用 <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>，媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>準備內容，廣告已插入時間軸，或廣告過程失敗。 可以開始緩衝或回放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已調用 <span class="codeph"> 玩</span>，所以TVSDK正在嘗試播放視頻。 在視頻實際播放之前可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>當應用程式播放和暫停媒體時，媒體播放器會在此狀態和 <span class="codeph"> PTMediaPlayerStatusPlaying</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>播放器到達流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，該播放器還會釋放任何相關的資源。 您不能再使用此實例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>進程期間出錯。 錯誤還可能會影響應用程式下一步的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關該進程的反饋（例如，在等待下一個狀態更改時使用旋轉器）或在播放媒體時採取下一步，例如在調用下一個方法之前等待適當的狀態。
