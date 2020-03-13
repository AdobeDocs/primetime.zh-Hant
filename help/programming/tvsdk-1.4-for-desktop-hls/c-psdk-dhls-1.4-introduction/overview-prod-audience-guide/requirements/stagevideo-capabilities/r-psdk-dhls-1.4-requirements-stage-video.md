---
description: 在支援GPU（硬體）加速的裝置上，您可使用flash.media.StageVideo物件，直接在裝置硬體上處理視訊。
seo-description: 在支援GPU（硬體）加速的裝置上，您可使用flash.media.StageVideo物件，直接在裝置硬體上處理視訊。
seo-title: StageVideo最低需求
title: StageVideo最低需求
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo最低需求{#stagevideo-minimum-requirements}

在支援GPU（硬體）加速的裝置上，您可使用flash.media.StageVideo物件，直接在裝置硬體上處理視訊。

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

不同因素的組合決定了您的使用時間和方式 `StageVideo`。 下表提供使用StageVideo時相關的一些要求和限制的快照。 這些規定和限制可能會有所變更。

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 平台 </th> 
   <th colname="col2" class="entry"> Windows和Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash Player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">至少Flash 10.1或更新版本 </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">針對後援軟體功能，請使用Flash 15和更新版本 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">瀏覽器和 <span class="codeph"> wmode設定</span> </td> 
   <td colname="col2"> <p><b>在Flash 15上</b>，設定 <span class="codeph"> wmode=opaque</span> ，讓您可以使用HTML覆蓋。 </p> <p>下列瀏覽器目前不支援硬體加速： 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Microsoft Windows版Mozilla Firefox </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Windows XP和Vista上26歲之前的Google Chrome及任何Chrome版本 </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer（所有版本） </li> 
     </ul>其他瀏覽器／作業系統組合可能會妨礙硬體加速的存取。 在這些情況下， <span class="codeph"></span> StageVideo會回落至軟體，對效能造成負面影響。 </p> <p><b>在Flash 14和舊版中</b>，如果瀏覽器不支援硬體加速，Flash Player可直接演算至GPU，但設定 <span class="codeph"> wmode=direct</span> ，以啟用此演算。 <p>提示： 2009年以上的GPU驅動程式可能需要更新，因為這些驅動程式可能缺乏硬體加速支援。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> NetStream對象 </td> 
   <td colname="col2">除非 <span class="codeph"> 將NetStream物件附加至StageVideo物件，否則不會傳送StageVideoEvent.RENDER_STATE</span> 事件 <span class="codeph"></span><span class="codeph"></span> 。 </td> 
  </tr> 
 </tbody> 
</table>

