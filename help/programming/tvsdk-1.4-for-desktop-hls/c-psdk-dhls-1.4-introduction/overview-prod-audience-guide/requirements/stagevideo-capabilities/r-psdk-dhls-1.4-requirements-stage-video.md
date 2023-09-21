---
description: 在支援GPU （硬體）加速的裝置上，您可以使用flash.media.StageVideo物件直接在裝置硬體上處理視訊。
title: StageVideo最低需求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# StageVideo最低需求{#stagevideo-minimum-requirements}

在支援GPU （硬體）加速的裝置上，您可以使用flash.media.StageVideo物件直接在裝置硬體上處理視訊。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的組合決定了您何時及如何使用 `StageVideo`. 下表提供使用StageVideo相關的一些需求和限制的快照。 這些需求和限制可能會有所變更。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Platform </th> 
   <th colname="col2" class="entry"> Windows與Mac作業系統 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash播放器 </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash10.1或更新版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">如需軟體功能的遞補內容，請參閱Flash15和更新版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">瀏覽器和 <span class="codeph"> wmode</span> 設定 </td> 
   <td colname="col2"> <p><b>在Flash15上</b>，設定 <span class="codeph"> wmode=opaque</span> 以便使用HTML覆蓋圖。 </p> <p>下列瀏覽器目前不支援硬體加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows上的Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">26以前的Google Chrome以及Windows XP和Vista上的任何版本Chrome </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer （所有版本） </li> 
     </ul>其他瀏覽器/作業系統組合可能會阻止存取硬體加速。 在這些案例中， <span class="codeph"> StageVideo</span> 退回至軟體，對效能造成負面影響。 </p> <p><b>在Flash14和更早版本上</b>，如果瀏覽器不支援硬體加速，Flash播放器可以直接轉譯至GPU，但需設定 <span class="codeph"> wmode=direct</span> 以啟用此演算。 <p>提示：2009年以前的GPU驅動程式可能需要更新，因為這些驅動程式可能缺乏硬體加速支援。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> netstream物件 </td> 
   <td colname="col2">此 <span class="codeph"> stagevideoevent.RENDER_STATE</span> 除非您附加 <span class="codeph"> NetStream</span> 物件至 <span class="codeph"> StageVideo</span> 物件。 </td> 
  </tr> 
 </tbody> 
</table>
