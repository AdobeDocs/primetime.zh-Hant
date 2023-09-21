---
description: PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。
title: 使用MediaPlayer物件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 使用MediaPlayer物件{#work-with-mediaplayer-objects}

PTMediaPlayer物件代表您的媒體播放器。 PTMediaPlayerItem代表播放器上的音訊或視訊。

## 關於MediaPlayerItem類別 {#section_B6F36C0462644F5C932C8AA2F6827071}

成功載入媒體資源後，TVSDK會建立 `PTMediaPlayerItem` 類別以提供對該資源的存取權。

此 `PTMediaPlayer` 解析媒體資源、載入關聯的資訊清單檔案，並剖析資訊清單。 這是資源載入程式的非同步部分。 此 `PTMediaPlayerItem` 執行個體會在資源解析後產生，此執行個體是媒體資源的解析版本。 TVSDK提供新建立專案的存取權 `PTMediaPlayerItem` 執行個體至 `PTMediaPlayer.currentItem`.

>[!TIP]
>
>您必須先等候資源成功載入，才能存取媒體播放器專案。

## MediaPlayer物件生命週期 {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

從您建立 `PTMediaPlayer` 例證直到您終止（重複使用或移除）它時，此例證會完成從一種狀態到另一種狀態的一系列轉變。

只有播放器處於特定狀態時，才允許進行某些操作。 例如，呼叫 `play` 在 `PTMediaPlayerStatusCreated` 是不允許的。 只有在播放器達到 `PTMediaPlayerStatusReady` 狀態。

若要使用狀態：

* 您可以使用擷取MediaPlayer物件的目前狀態 `PTMediaPlayer.status`.
* 狀態清單定義於 `PTMediaPlayerStatus`.

MediaPlayer例項生命週期的狀態轉換圖：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

下表提供其他詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> PTMediaPlayerStatus </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式呼叫來要求新的媒體播放器 <span class="codeph"> playerWithMediaPlayerItem</span>. 新建立的播放器正等待您指定媒體播放器專案。 這是媒體播放器的初始狀態。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式呼叫 <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>，且媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>內容已準備且廣告已插入時間軸中，或廣告程式失敗。 緩衝或播放可以開始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> play</span>，因此TVSDK正在嘗試播放視訊。 在視訊實際播放之前，可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態與之間移動 <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>播放器到達資料流結尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>您的應用程式已發行媒體播放器，也會發行任何相關資源。 您無法再使用此例項 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>處理期間發生錯誤。 錯誤也可能會影響您的應用程式下一步可以執行的動作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供程式的意見回饋（例如，在等候下一個狀態變更時執行旋轉圖示），或是在播放媒體時執行下一個步驟，例如在呼叫下一個方法之前等候適當的狀態。
