---
description: 在支援GPU（硬體）加速的裝置上，您可使用flash.media.StageVideo物件，直接在裝置硬體上處理視訊。
title: StageVideo最低需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# StageVideo最低需求{#stagevideo-minimum-requirements}

在支援GPU（硬體）加速的裝置上，您可使用flash.media.StageVideo物件，直接在裝置硬體上處理視訊。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的組合決定了您可以使用`StageVideo`的時間和方式。 下表提供使用StageVideo時相關的一些要求和限制的快照。 這些規定和限制可能會有所變更。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 平台 </th> 
   <th colname="col2" class="entry"> Windows和Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash播放器 </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash10.1或更新版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">針對軟體後援功能，請Flash15和更新版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">瀏覽器和<span class="codeph"> wmode</span>設定 </td> 
   <td colname="col2"> <p><b>在Flash15中</b>，設定 <span class="codeph"> wmode=</span> opaqueso，您就可以使用HTML覆蓋。 </p> <p>下列瀏覽器目前不支援硬體加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows版Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Windows XP和Vista上26歲之前的Google Chrome及任何Chrome版本 </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer（所有版本） </li> 
     </ul>其他瀏覽器／作業系統組合可能會妨礙硬體加速的存取。 在這些情況下，<span class="codeph"> StageVideo</span>會回落至對效能有負面影響的軟體。 </p> <p><b>在Flash14和舊版中</b>，如果瀏覽器不支援硬體加速，Flash播放器可直接演算至GPU，但設定 <span class="codeph"> wmode=</span> directto啟用此演算。 <p>提示： 2009年以上的GPU驅動程式可能需要更新，因為這些驅動程式可能缺乏硬體加速支援。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream對象 </td> 
   <td colname="col2">除非您將<span class="codeph"> NetStream</span>物件附加至<span class="codeph"> StageVideo</span>物件，否則不會傳送<span class="codeph"> StageVideoEvent.RENDER_STATE</span>事件。 </td> 
  </tr> 
 </tbody> 
</table>

