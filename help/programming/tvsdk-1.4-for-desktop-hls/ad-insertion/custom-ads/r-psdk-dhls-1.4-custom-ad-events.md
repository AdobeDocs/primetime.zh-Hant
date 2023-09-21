---
description: TVSDK播放器會傳送事件以顯示自訂廣告載入狀態，或忽略載入時間過長或有錯誤的廣告。 這些事件是在events.CustomAdEvents中定義。
title: 自訂廣告事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# 自訂廣告事件{#custom-ad-events}

TVSDK播放器會傳送事件以顯示自訂廣告載入狀態，或忽略載入時間過長或有錯誤的廣告。 這些事件是在events.CustomAdEvents中定義。

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
   <td colname="col1"> <span class="codeph"> adloaded </span> </td> 
   <td colname="col2"> 自訂廣告已載入。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> 正在載入自訂廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已暫停廣告 </span> </td> 
   <td colname="col2"> 自訂廣告已暫停。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> 自訂廣告在暫停後繼續播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> 正在播放自訂廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>自訂廣告播放器會通知TVSDK播放器自訂廣告的進度。 &amp;nbsp； </p> <p>此 <span class="codeph"> currenttime </span> 和 <span class="codeph"> totalTime </span> 的廣告會與此事件一併傳遞。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已開始 </td> 
   <td colname="col2"> 自訂廣告已開始播放，並對檢視器顯示。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> 自訂廣告已播放完畢。 </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
