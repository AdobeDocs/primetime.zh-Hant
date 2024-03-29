---
description: 從您建立MediaPlayer例項的那一刻到您終止（重複使用或移除）該例項的那一刻，此例項會完成狀態之間的一系列轉換。
title: MediaPlayer物件生命週期
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# MediaPlayer物件生命週期{#mediaplayer-object-lifecycle}

從您建立MediaPlayer例項的那一刻到您終止（重複使用或移除）該例項的那一刻，此例項會完成狀態之間的一系列轉換。

只有播放器處於特定狀態時，才允許進行某些操作。 例如，呼叫 `play` 不允許在IDLE中使用。 只有在播放器達到「已準備」狀態後，您才能呼叫此狀態。

若要使用狀態：

* 您可以擷取 `MediaPlayer` 物件，使用 `MediaPlayer.status` 屬性。

  ```
  function get status():String;
  ```

* 狀態清單定義於 `MediaPlayer.PlayerStatus`.

生命週期的狀態轉換圖 `MediaPlayer` 例項：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

下表提供其他詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus </span> </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 閒置 </span> </td> 
   <td colname="col2"> <p> 您的應用程式正在具現化以請求新的媒體播放器 <span class="codeph"> MediaPlayer </span>. 新建立的播放器正等待您指定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在初始化 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> MediaPlayer.replaceCurrentResource </span>，且媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化 </span> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器專案。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在準備 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> MediaPlayer.prepareToPlay </span>. 媒體播放器正在載入媒體播放器專案和相關資源。 </p> <p>提示：可能會發生主要媒體的某些緩衝。 </p> <p>TVSDK正在準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 </p> <p>提示：若要將開始時間設為非零值，請呼叫 <span class="codeph"> prepareToPlay(startTime) </span> 以毫秒為單位的時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已準備 </span> </td> 
   <td colname="col2"> <p>內容已準備且廣告已插入時間軸中，或廣告程式失敗。 緩衝或播放可以開始。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 正在播放 </span> </td> 
   <td colname="col2"> <p>您的應用程式已呼叫 <span class="codeph"> play </span>，因此TVSDK正在嘗試播放視訊。 在視訊實際播放之前，可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停 </span> </td> 
   <td colname="col2"> <p>當您的應用程式播放和暫停媒體時，媒體播放器會在此狀態與「正在播放」之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 搜尋 </span> </td> 
   <td colname="col2"> <p>媒體播放器暫停或播放時，正在尋找正確位置。 若要判斷搜尋何時開始或結束，請聆聽 <span class="codeph"> SeekEvent.SEEK_BEGIN </span> 和 <span class="codeph"> SeekEvent.SEEK_END </span> 事件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已完成 </span> </td> 
   <td colname="col2"> <p>播放器到達資料流結尾，且播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已發行 </span> </td> 
   <td colname="col2"> <p>您的應用程式已發行媒體播放器，也會發行任何相關資源。 您無法再使用此例項 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 錯誤 </span> </td> 
   <td colname="col2"> <p>處理期間發生錯誤。 錯誤也可能會影響您的應用程式下一步可以執行的動作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供程式的意見回饋（例如，在等候下一個狀態變更時執行旋轉圖示），或是在播放媒體時執行下一個步驟，例如在呼叫下一個方法之前等候適當的狀態。
