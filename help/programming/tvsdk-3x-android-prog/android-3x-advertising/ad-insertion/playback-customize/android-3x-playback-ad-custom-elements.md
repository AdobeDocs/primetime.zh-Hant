---
description: TVSDK提供的類別與方法可用於自訂包含廣告之內容的播放行為。
title: 廣告播放的API元素
exl-id: 1114d00b-e853-47a5-af29-253df615692e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 廣告播放的API元素 {#api-elements-for-ad-playback}

TVSDK提供的類別與方法可用於自訂包含廣告之內容的播放行為。

下列API元素對於自訂播放很實用：

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>API元素 </b></th> 
   <th colname="col2" class="entry"> <b>支援廣告的內容</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">控制廣告插播是否應該標示為已被檢視者觀看，如果是，何時標示為。 使用設定並取得追蹤原則 <span class="codeph"> setAdBreakAsWatched</span> 和 <span class="codeph"> getAdBreakAsWatched</span>. </td> 
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
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> 允許自訂TVSDK廣告行為的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> 實作預設TVSDK行為的類別。 您的應用程式可以覆寫此類別來自訂預設行為，而無需實作完整的介面。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>這是播放的當地時間，不包括置入的廣告插播。 </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>在此處，搜尋會相對於資料流中的當地時間進行。 </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>時間軸上的虛擬位置會轉換為本機位置。 </p> </li> 
    </ul> <p>重要：  <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> MediaPlayer</span> 傳回相對於原始內容的目前時間，不含動態拼接的廣告。 <span class="codeph"> getLocalTime</span> 在 <span class="codeph"> 廣告插播</span> 傳回相對於原始內容的分隔開始時間。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> 廣告插播</span> </td> 
   <td colname="col2"><span class="codeph"> iswatched</span> 屬性。 指出檢視器是否觀看過廣告。 </td> 
  </tr> 
 </tbody> 
</table>
