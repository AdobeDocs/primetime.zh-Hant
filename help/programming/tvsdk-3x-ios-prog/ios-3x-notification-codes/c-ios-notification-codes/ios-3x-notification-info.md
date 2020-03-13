---
description: 此表提供了有關INFO類型通知的詳細資訊。
seo-description: 此表提供了有關INFO類型通知的詳細資訊。
seo-title: 資訊通知代碼
title: 資訊通知代碼
uuid: 21297863-dac1-45a4-ac9d-309d1f746f8b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 資訊通知代碼 {#info-notification-codes}

此表提供了有關INFO類型通知的詳細資訊。

大部分資訊性通知都包含相關的中繼資料，例如無法下載的資源URL。 有些通知包含中繼資料，以指定問題是發生在主要視訊內容、替代音訊內容或廣告中。

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>程式碼</b></th> 
   <th colname="2" class="entry"><b>名稱</b></th> 
   <th colname="3" class="entry"><b>內部通知</b></th> 
   <th colname="4" class="entry"><b>中繼資料索引鍵</b></th> 
   <th colname="5" class="entry"><b>注釋</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 播放已開始。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <p> 無 </p> </td> 
   <td colname="5"> 已啟動搜索操作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> 搜索操作已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> 播放器狀態已變更。 當狀態為ERROR時，內部通知是觸發交換機到ERROR狀態的錯誤通知對象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>可調式位元速率(ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> 位元速率變更 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 位元速率 </span> </td> 
   <td colname="5"> 視訊的位元速率已變更。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>延遲系結音訊(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>音軌已變更。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>字幕</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>字幕音軌變了。 </p> </td> 
  </tr> 
 </tbody> 
</table>