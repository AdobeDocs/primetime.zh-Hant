---
description: TVSDK提供您可用來自訂包含廣告之內容的播放行為的類別和方法。
title: 廣告播放的API元素
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 廣告播放{#api-elements-for-ad-playback}的API元素

TVSDK提供您可用來自訂包含廣告之內容的播放行為的類別和方法。

下列API元素對於自訂播放非常有用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API元素 </th> 
   <th colname="col2" class="entry"> 支援廣告的內容 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata  </span> </td> 
   <td colname="col2">控制廣告插播是否應標示為已被檢視者觀看，如果是，應於何時標籤。 使用<span class="codeph"> setAdBreakAsWatched</span>和<span class="codeph"> getAdBreakAsWatched</span>來設定並取得監看原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> 列舉廣告插播的可能播放原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> 列舉廣告的可能播放原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector  </span> </td> 
   <td colname="col2"> 允許自訂TVSDK廣告行為的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> 實作預設TVSDK行為的類別。 您的應用程式可以覆寫此類別，以自訂預設行為，而不需實作完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>這是播放的本機時間，排除已置入的廣告插播。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>。 <p>在此，搜索相對於流中的本地時間發生。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>。 <p>時間軸上的虛擬位置會轉換為本機位置。 </p> </li> 
    </ul> <p>重要： <span class="codeph">在<span class="codeph"> MediaPlayer</span>中的getLocalTime</span>會傳回目前相對於原始內容的時間，而不會動態拼接廣告。 <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreak傳回中斷相對於原始內容的開始時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty。指出檢視者是否已觀看廣告。 </td> 
  </tr> 
 </tbody> 
</table>

