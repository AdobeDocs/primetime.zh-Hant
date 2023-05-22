---
description: 從您建立MediaPlayer實例的一刻到終止（重用或刪除）它的一刻，此實例完成狀態之間的一系列過渡。
title: MediaPlayer對象生命週期
exl-id: 0f2f3699-b745-4b14-8b7e-68696960ccab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# MediaPlayer對象生命週期{#mediaplayer-object-lifecycle}

從您建立MediaPlayer實例的一刻到終止（重用或刪除）它的一刻，此實例完成狀態之間的一系列過渡。

僅當播放器處於特定狀態時才允許某些操作。 例如，調用 `play` 不允許使用IDLE。 僅當播放器達到PREPARED狀態後才可調用此狀態。

要使用狀態，請執行以下操作：

* 可以檢索 `MediaPlayer` 對象 `MediaPlayer.status` 屬性。

   ```
   function get status():String;
   ```

* 狀態清單在中定義 `MediaPlayer.PlayerStatus`。

生命週期的狀態轉換圖 `MediaPlayer` 實例：
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

下表提供了更多詳細資訊：

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> 媒體播放器狀態 </span> </th> 
   <th colname="col2" class="entry"> 在 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 空閒 </span> </td> 
   <td colname="col2"> <p> 應用程式通過實例化請求了新媒體播放器 <span class="codeph"> 媒體播放器 </span>。 新建立的播放器正在等待您指定媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 初始化 </span> </td> 
   <td colname="col2"> <p>您的應用程式已調用 <span class="codeph"> MediaPlayer.replaceCurrentResource </span>，媒體播放器正在載入。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已初始化 </span> </td> 
   <td colname="col2"> <p>TVSDK已成功設定媒體播放器項。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 準備 </span> </td> 
   <td colname="col2"> <p>您的應用程式已調用 <span class="codeph"> MediaPlayer.prepareToPlay </span>。 媒體播放器正在載入媒體播放器項目和相關資源。 </p> <p>提示：可能會發生主媒體的緩衝。 </p> <p>TVSDK正在準備媒體流並嘗試執行廣告解析和廣告插入（如果已啟用）。 </p> <p>提示：要將開始時間設定為非零值，請調用 <span class="codeph"> 準備播放（開始時間） </span> 以毫秒為單位。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 準備 </span> </td> 
   <td colname="col2"> <p>準備內容，廣告已插入時間軸，或廣告過程失敗。 可以開始緩衝或回放。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 播放 </span> </td> 
   <td colname="col2"> <p>您的應用程式已調用 <span class="codeph"> 玩 </span>，所以TVSDK正在嘗試播放視頻。 在視頻實際播放之前可能會發生一些緩衝。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停 </span> </td> 
   <td colname="col2"> <p>當應用程式播放和暫停媒體時，媒體播放器會在此狀態和播放之間移動。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 尋找 </span> </td> 
   <td colname="col2"> <p>媒體播放器在暫停或播放時正在尋找正確的位置。 要確定搜索何時開始或結束，請收聽 <span class="codeph"> SeekEvent.SEEK_BEGIN </span> 和 <span class="codeph"> SeekEvent.SEEK_END </span> 事件。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已完成 </span> </td> 
   <td colname="col2"> <p>播放器到達流的末尾，播放已停止。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已發佈 </span> </td> 
   <td colname="col2"> <p>您的應用程式已發佈媒體播放器，該播放器還會釋放任何相關的資源。 您不能再使用此實例 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 錯誤 </span> </td> 
   <td colname="col2"> <p>進程期間出錯。 錯誤還可能會影響應用程式下一步的操作。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>您可以使用狀態來提供有關該進程的反饋（例如，在等待下一個狀態更改時使用旋轉器）或在播放媒體時採取下一步，例如在調用下一個方法之前等待適當的狀態。
