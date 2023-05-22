---
description: TVSDK提供可用於自定義包含廣告的內容的播放行為的類和方法。
title: 用於廣告播放的API元素
exl-id: a976a905-8aa2-4bdb-9e10-addb65a433ef
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 用於廣告播放的API元素 {#api-elements-for-ad-playback}

TVSDK提供可用於自定義包含廣告的內容的播放行為的類和方法。

以下API元素對自定義回放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支援廣告的內容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> 廣告元資料</span> </td> 
   <td colname="col2">控制廣告分段是否應被標籤為已被觀眾觀看，如果是，何時標籤。 使用設定和獲取監視策略 <span class="codeph"> setAdBreakAsStated</span> 和 <span class="codeph"> getAdBreakAsStated</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreak策略</span> </td> 
   <td colname="col2"> 枚舉廣告中斷的可能回放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 廣告策略</span> </td> 
   <td colname="col2"> 枚舉廣告可能的播放策略。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> 允許自定義TVSDK廣告行為的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> 實現預設TVSDK行為的類。 您的應用程式可以覆蓋此類，以自定義預設行為而不實施完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 媒體播放器</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span>。 <p>這是回放的本地時間，不包括放置的廣告分段。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> 查找到本地</span>。 <p>此處，查找相對於流中的本地時間發生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>。 <p>時間線上的虛擬位置被轉換為本地位置。 </p> </li> 
    </ul> <p>重要提示：  <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> 媒體播放器</span> 返回相對於原始內容的當前時間，而不動態拼接廣告。 <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> 廣告中斷</span> 返回中斷相對於原始內容的開始時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 廣告中斷</span> </td> 
   <td colname="col2"><span class="codeph"> 已監視</span> 屬性。 指示查看者是否已觀看廣告。 </td> 
  </tr> 
 </tbody> 
</table>
