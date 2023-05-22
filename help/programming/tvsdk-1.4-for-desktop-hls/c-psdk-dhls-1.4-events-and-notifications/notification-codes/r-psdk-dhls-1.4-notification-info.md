---
description: 此表提供了有關INFO類型通知的詳細資訊。
title: INFO通知代碼
exl-id: 6f813797-b4ef-4e75-a096-d55103b7304b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 4%

---

# INFO通知代碼{#info-notification-codes}

此表提供了有關INFO類型通知的詳細資訊。

## 節標題 {#section_ED4302E363AE48CBA2C3E0B71AE612D8}

大多數資訊性通知都包含相關的元資料，例如，無法下載的資源的URL。 某些通知包含元資料，用於指定是在主視頻內容、備用音頻內容還是廣告中出現問題。

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 代碼 </th> 
   <th colname="2" class="entry"> 名稱 </th> 
   <th colname="3" class="entry"> 內部通知 </th> 
   <th colname="4" class="entry"> 元資料鍵 </th> 
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
   <td colname="2"><span class="codeph"> 播放開始 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 播放已開始。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> 播放完成 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> 無 </td> 
   <td colname="5"> 播放已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> 查找開始 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 查找時間</span> </td> 
   <td colname="5"> 已啟動查找操作。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> 查找完成 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"><span class="codeph"> 查找時間</span> </td> 
   <td colname="5"> 搜索操作已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300004 </span> </td> 
   <td colname="2"><span class="codeph"> 內容更改 </span> </td> 
   <td colname="3"> 無 </td> 
   <td colname="4"> <span class="codeph"> 內容ID</span> <span class="codeph"> 當前媒體時間</span> </td> 
   <td colname="5"> 當前播放時間已越過主內容和備用內容之間的邊框。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> 播放器_狀態_更改 </span> </td> 
   <td colname="3"> <p>任何錯誤通知。 </p> </td> 
   <td colname="4"><span class="codeph"> 狀態 </span> </td> 
   <td colname="5"> 玩家狀態已更改。 當狀態為ERROR時，內部通知是觸發交換機進入ERROR狀態的錯誤通知對象。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300100 </span> </td> 
   <td colname="2"><span class="codeph"> 載入資訊可用 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> 片段URL</span> <span class="codeph"> 片段大小</span> <span class="codeph"> FRAGMENT_DOWNLOAD_DURATION</span> <span class="codeph"> PERIOD_INDEX</span> </td> 
   <td colname="5"> 提供與視頻段下載方式相關的資訊。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300101 </span> </td> 
   <td colname="2"><span class="codeph"> 視頻大小更改 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> 高度</span> <p><span class="codeph"> 寬度</span> </p> </td> 
   <td colname="5"> 視頻播放窗口的大小已更改。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>自適應比特率(ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> 比特率_更改 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 比特率 </span><span class="codeph"> 當前媒體時間 </span> </td> 
   <td colname="5"> 視頻的比特率已更改。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>廣告處理 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303000 </span> </td> 
   <td colname="2"><span class="codeph"> 時間軸_更改 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 內容ID </span><span class="codeph"> PERIOD_INDEX </span> </td> 
   <td colname="5"> 時間線已更改（例如，添加或刪除了備用內容）。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_放置_完成 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> 建議的_AD_BREAK</span> <span class="codeph"> 接受_AD_BREAK</span> </td> 
   <td colname="5"> TVSDK接受了建議的廣告中斷，並將其全部或部分放在播放時間線上。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303002 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_START </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 已開始播放特定廣告分段。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_BREAK_COMPLETE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> AD_BREAK </span> </td> 
   <td colname="5"> 播放特定廣告片段已完成。 </td> 
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
   <td colname="2"><span class="codeph"> 完成(_C) </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> </td> 
   <td colname="5"> 播放特定廣告已完成。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 303006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_PROGRESS </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <span class="codeph"> AD_BREAK</span> <p><span class="codeph"> 廣告</span> </p> <span class="codeph"> 進度</span> </td> 
   <td colname="5"> 某個廣告的播放量已達到該特定廣告的一定百分比。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>後期綁定音頻(LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"><span class="codeph"> 跟蹤ID </span><span class="codeph"> 當前媒體時間 </span> </td> 
   <td colname="5"> <p>音頻軌道已更改。 </p> </td> 
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
   <td colname="5"> <p>新DRM資料可用。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>泛型</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 399999 </span> </td> 
   <td colname="2"><span class="codeph"> 泛型資訊 </span> </td> 
   <td colname="3"> <p>無 </p> </td> 
   <td colname="4"> <p>無 </p> </td> 
   <td colname="5"> <p>標籤泛型資訊事件。 不是TVSDK發的。 它只是TVSDK資訊事件所對應的數字代碼範圍的結束的標誌。 </p> </td> 
  </tr> 
 </tbody> 
</table>
