---
description: 此表提供了有關INFO的詳細資訊。 類型通知。
seo-description: 此表提供了有關INFO的詳細資訊。 類型通知。
seo-title: 資訊通知代碼
title: 資訊通知代碼
uuid: 2b9f9328-4e09-44b7-8ea5-237c46e65e73
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 資訊通知代碼{#info-notification-codes}

此表提供了有關INFO的詳細資訊。 類型通知。

<!--<a id="section_ED4302E363AE48CBA2C3E0B71AE612D8"></a>-->

大部分資訊性通知都包含相關的中繼資料，例如無法下載的資源URL。 有些通知包含中繼資料，以指定問題是發生在主要視訊內容、替代音訊內容或廣告中。

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 程式碼 </th> 
   <th colname="2" class="entry"> 名稱 </th> 
   <th colname="3" class="entry"> 內部通知 </th> 
   <th colname="4" class="entry"> 中繼資料索引鍵 </th> 
   <th colname="5" class="entry"> 注釋 </th> 
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
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> 已啟動搜索操作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> SEEK_TIME</span> </td> 
   <td colname="5"> 搜索操作已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_CHANGE </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> CONTENT_ID</span><span class="codeph"> CURRENT_MEDIA_TIME</span> </td> 
   <td colname="5"> 目前的播放時間已跨越主要內容與替代內容之間的邊界。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>任何錯誤通知。 </p> </td> 
   <td colname="4"><span class="codeph"> 州 </span> </td> 
   <td colname="5"> 播放器狀態已變更。 當狀態為ERROR時，內部通知是觸發交換機到ERROR狀態的錯誤通知對象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300006 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_MARKER </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 收到內容標籤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> LOAD_INFO_AVAILABLE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> FRAGMENT_URL</span><span class="codeph"> FRAGMENT_SIZE</span> FRAGMENT_DOWNLOAD_DURATION <span class="codeph"></span><span class="codeph"> PERIOD_INDEX</span> </td> 
   <td colname="5"> 提供視訊區段下載方式的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> VIDEO_SIZE_CHANGED </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> 高度</span> <p><span class="codeph"> 寬度</span> </p> </td> 
   <td colname="5"> 視訊播放視窗的大小已變更。 </td> 
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
   <td colname="4"><span class="codeph"> 位元 </span><span class="codeph"> 速率CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 視訊的位元速率已變更。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告處理</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> 時間軸_變更 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span><span class="codeph"> PERIOD_INDEX </span> </td> 
   <td colname="5"> 時間軸已變更（例如，已新增或移除替代內容）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_PLACEMENT_COMPLETE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> PUSHED_AD_BREAK</span> ACCEPTED <span class="codeph"> _AD_BREAK</span> </td> 
   <td colname="5"> 建議的廣告插播已獲得 <code>primetime-sdk-name</code> 播放時間軸的接受並放置（完整或部分）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 特定廣告插播的播放已開始。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 特定廣告插播的播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303004 </span> </td> 
   <td colname="2"><span class="codeph"> AD_START </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> </td> 
   <td colname="5"> 已開始播放特定廣告。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_COMPLETE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> </td> 
   <td colname="5"> 特定廣告的播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> <span class="codeph"> 進度</span> </td> 
   <td colname="5"> 特定廣告的播放已達到該特定廣告的特定百分比。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303007 </span> </td> 
   <td colname="2"><span class="codeph"> TIMED_METADATA_ADD </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> 類型</span> <p><span class="codeph"> ID</span> </p> <span class="codeph"> 名稱</span> <p><span class="codeph"> 時間</span> </p> </td> 
   <td colname="5"> 資訊清單中發現新的計時中繼資料。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303008 </span> </td> 
   <td colname="2"><span class="codeph"> AD_CLICK </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 傳回使用者所點按之廣告的相關資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303009</span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_BRIKPED</span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> <span class="codeph"> AD_CLICK</span> </td> 
   <td colname="5"> 已略過廣告插播。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname=""><b>延遲系結音訊(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> TRACK_ID </span><span class="codeph"> CURRENT_MEDIA_TIME </span> </td> 
   <td colname="5"> 音軌已變更。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 305000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_METADATA_AVAILABLE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> PREFETCH_TIMESTAMP </span> </td> 
   <td colname="5"> 有新的DRM資料可供使用。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_INFO </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>標籤一般資訊事件。 並非由TVSDK實際核發。 它只是TVSDK資訊事件所對應數值代碼範圍結尾的標籤。 </p> </td> 
  </tr> 
 </tbody> 
</table>

