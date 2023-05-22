---
description: 在支援GPU（硬體）加速的設備上，可以使用flash.media.StageVideo對象直接在設備硬體上處理視頻。
title: StageVideo最低要求
exl-id: f401682d-c47d-4284-8832-293515a76581
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# StageVideo最低要求{#stagevideo-minimum-requirements}

在支援GPU（硬體）加速的設備上，可以使用flash.media.StageVideo對象直接在設備硬體上處理視頻。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

各種因素的組合決定了您何時以及如何使用 `StageVideo`。 下表顯示了與使用StageVideo相關的一些要求和限制的快照。 這些要求和限制可能會改變。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 平台 </th> 
   <th colname="col2" class="entry"> Windows和Mac作業系統 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash10.1或更高版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">對於軟體功能的回退，Flash15及更高版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">瀏覽器和 <span class="codeph"> wmode（w模式）</span> 設定 </td> 
   <td colname="col2"> <p><b>關於Flash15</b>。 <span class="codeph"> wmode=opaque</span> 這樣你就能用HTML疊層。 </p> <p>以下瀏覽器當前不支援硬體加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">MicrosoftWindows上的Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">GoogleChrome 26之前和Windows XP和Vista上任何版本的Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">MicrosoftInternet Explorer（所有版本） </li> 
     </ul>其他瀏覽器/作業系統組合可能會阻止對硬體加速的訪問。 在這些情景中， <span class="codeph"> 舞台視頻</span> 退回到對效能有負面影響的軟體。 </p> <p><b>關於第14號Flash及其之前</b>，如果瀏覽器不支援硬體加速，則Flash播放器可以直接呈現到GPU，但可以設定 <span class="codeph"> wmode=direct</span> 啟用此呈現。 <p>提示：需要更新2009年以前的GPU驅動程式，因為這些驅動程式可能不支援硬體加速。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream對象 </td> 
   <td colname="col2">的 <span class="codeph"> StageVideoEvent.RENDER_STATE</span> 除非您附加 <span class="codeph"> NetStream</span> 對象 <span class="codeph"> 舞台視頻</span> 的雙曲餘切值。 </td> 
  </tr> 
 </tbody> 
</table>
