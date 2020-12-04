---
description: 從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。
seo-description: 從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。
seo-title: MediaPlayer物件生命週期
title: MediaPlayer物件生命週期
uuid: 1452ae3a-7ce9-439e-951c-9d3db63b1d20
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---


# MediaPlayer物件生命週期{#mediaplayer-object-lifecycle}

從您建立MediaPlayer例項到您終止（重複使用或移除）該例項時，此例項會完成狀態間的一系列轉換。

某些操作僅在播放器處於特定狀態時才允許。 例如，不允許在IDLE中調用`play`。 您只有在播放器達到PREPARED狀態後，才可呼叫此狀態。

要使用狀態：

* 可以使用`MediaPlayer.status`屬性來檢索`MediaPlayer`對象的當前狀態。

   ```
   function get status():String;
   ```

* 狀態清單在`MediaPlayer.PlayerStatus`中定義。

`MediaPlayer`實例生命週期的狀態轉移圖：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

下表提供其他詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus  </span> </th> 
   <th colname="col2" class="entry"> 發生於 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 空閒  </span> </td> 
   <td colname="col2"> <p> 您的應用程式會執行個體化<span class="codeph"> MediaPlayer </span>，以請求新的媒體播放器。 新建立的播放器正在等候您指定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 初始化  </span> </td> 
   <td colname="col2"> <p>您的應用程式名為<span class="codeph"> MediaPlayer.replaceCurrentResource </span>，且媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化  </span> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項目。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 準備  </span> </td> 
   <td colname="col2"> <p>您的應用程式名為<span class="codeph"> MediaPlayer.prepareToPlay </span>。 媒體播放器正在載入媒體播放器項目和相關資源。 </p> <p>提示： 可能會發生主媒體的緩衝。 </p> <p>TVSDK正在準備媒體串流，並嘗試執行廣告解析和廣告插入（如果已啟用）。 </p> <p>提示： 要將開始時間設定為非零值，請調用<span class="codeph"> prepareToPlay(startTime)</span>，時間以毫秒為單位。 </p> </td> 
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
   <td colname="col1"> <span class="codeph"> 搜尋  </span> </td> 
   <td colname="col2"> <p>媒體播放器在暫停或播放時會尋找正確位置。 要確定搜索何時開始或結束，請監聽<span class="codeph"> SeekEvent.SEEK_BEGIN </span>和<span class="codeph"> SeekEvent.SEEK_END </span>事件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已完成  </span> </td> 
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
>您可以使用狀態來提供有關程式的意見回應（例如，在等待下一個狀態變更時使用微調按鈕），或在播放媒體時採取下一步驟，例如在呼叫下一個方法之前等待適當的狀態。

