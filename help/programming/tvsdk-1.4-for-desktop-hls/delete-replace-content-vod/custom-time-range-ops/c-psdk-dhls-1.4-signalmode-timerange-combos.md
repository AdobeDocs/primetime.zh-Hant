---
title: 信令模式和時間範圍
description: 信令模式和時間範圍
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 信令模式和時間範圍{#signaling-mode-and-time-range}

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> 標籤 </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> 取代 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> CustomRange OpportunityGenerator  </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
    &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
      &nbsp;range.end,&nbsp; 
      &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ServerMap信 </span> 令模式 </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK&nbsp;); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE&nbsp;); 
    </code> </td> 
   <td> N/A（自動CustomRange信令模式） </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue信 </span> 令模式 </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> N/A（自動CustomRange信令模式） </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange信 </span> 令模式 </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement1&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
     placement2&nbsp;=&nbsp;placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(/ 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.MID_ROLL( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.PRE_ROLL), 
     &nbsp;&nbsp;&nbsp;&nbsp;rangeDuration, 
     &nbsp;&nbsp;&nbsp;&nbsp;placementMode 
     ); 
    </code> </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> 標籤 </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> 取代 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> AdSignalingMode OpportunityGenerator  </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end,&nbsp; 
     &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> SeverMap信 </span> 令模式 </td> 
   <td> 不存在（廣告已停用）。 </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.SERVER_MAP, 
     Placement.UNKNOWN_TIME, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/A（自動<span class="codeph"> CustomRange </span>信令模式） </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue信 </span> 令模式 </td> 
   <td> 不存在（廣告已停用）。 </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.PRE_ROLL, 
     playhead, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/A（自動<span class="codeph"> CustomRange </span>信令模式） </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange信 </span> 令模式 </td> 
   <td> 不存在（廣告已停用）。 </td> 
   <td> 無 </td> 
   <td> 無（已在<span class="codeph"> CustomRangeOpportunityGenerator </span>中處理） </td> 
  </tr> 
 </tbody> 
</table>
