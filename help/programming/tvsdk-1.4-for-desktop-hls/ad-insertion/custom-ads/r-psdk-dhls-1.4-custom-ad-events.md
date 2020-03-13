---
description: TVSDK播放器會派單事件以顯示自訂廣告載入狀態，或忽略載入時間太長或有錯誤的廣告。 這些事件在events.CustomAdEvents中定義。
seo-description: TVSDK播放器會派單事件以顯示自訂廣告載入狀態，或忽略載入時間太長或有錯誤的廣告。 這些事件在events.CustomAdEvents中定義。
seo-title: 自訂廣告事件
title: 自訂廣告事件
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 自訂廣告事件{#custom-ad-events}

TVSDK播放器會派單事件以顯示自訂廣告載入狀態，或忽略載入時間太長或有錯誤的廣告。 這些事件在events.CustomAdEvents中定義。

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 事件 </th> 
   <th colname="col2" class="entry"> 定義 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> 檢視器點按自訂廣告的次數。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> 自訂廣告發生錯誤。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> 自訂廣告已載入。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> 正在載入自訂廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> 自訂廣告已暫停。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResuted </span> </td> 
   <td colname="col2"> 暫停後，自訂廣告仍繼續播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> 自訂廣告正在播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>自訂廣告播放器會通知TVSDK播放器有關自訂廣告的進度。 &amp;nbsp; </p> <p>廣告 <span class="codeph"> 的目 </span> 前時 <span class="codeph"> 間和總 </span> 時間會隨此事件傳遞。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> 自訂廣告已開始播放，並會顯示給檢視器。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> 自訂廣告已播放完成。 </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

