---
description: TVSDK播放器調度事件以顯示自定義廣告載入狀態或忽略載入時間太長或出現錯誤的廣告。 這些事件在events.CustomAdEvents中定義。
title: 自定義廣告事件
exl-id: 44f32584-7f6c-4071-82b6-9cc9584418ee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# 自定義廣告事件{#custom-ad-events}

TVSDK播放器調度事件以顯示自定義廣告載入狀態或忽略載入時間太長或出現錯誤的廣告。 這些事件在events.CustomAdEvents中定義。

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 事件 </th> 
   <th colname="col2" class="entry"> 定義 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 廣告按一下通過 </span> </td> 
   <td colname="col2"> 查看器按一下自定義廣告的次數。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 廣告錯誤 </span> </td> 
   <td colname="col2"> 自定義廣告出錯。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已載入廣告 </span> </td> 
   <td colname="col2"> 已載入自定義廣告。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 廣告載入 </span> </td> 
   <td colname="col2"> 正在載入自定義廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 暫停廣告 </span> </td> 
   <td colname="col2"> 自定義廣告已暫停。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 已恢復 </span> </td> 
   <td colname="col2"> 暫停後，自定義廣告繼續播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 廣告播放 </span> </td> 
   <td colname="col2"> 正在播放自定義廣告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 廣告進度 </span> </td> 
   <td colname="col2"> <p>自定義廣告播放器將自定義廣告的進度通知TVSDK播放器。 &amp;nbsp; </p> <p>的 <span class="codeph"> 當前時間 </span> 和 <span class="codeph"> 總時間 </span> 廣告會與此事件一起傳遞。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已啟動 </td> 
   <td colname="col2"> 自定義廣告已開始播放，並將顯示給查看者。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 已停止 </td> 
   <td colname="col2"> 自定義廣告已播放完。 </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
