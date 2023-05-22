---
description: The version of EXT-X-VERSION in the .m3u8 file affects what features are available to your application and what EXT tags are valid in your playlist/manifest.
title: EXT-X-VERSION requirements
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X-VERSION requirements{#ext-x-version-requirements}

The version of #EXT-X-VERSION in the .m3u8 file affects what features are available to your application and what EXT tags are valid in your playlist/manifest.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

   [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)
* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

   [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)
* Adobe recommends using at least version 2 for playback in -based clients.

   Clients and servers must implement the versions in the following way:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Use at least this version </th> 
   <th colname="2" class="entry"> To use these features </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> <span class="codeph"></span> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph"></span> <p><span class="codeph"></span>Version 3 and above require durations to be exact in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"></span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6"><span class="codeph"></span> </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph"></span> </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD"><span class="codeph"></span> </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph"></span> </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">的 <span class="codeph"> 音頻 </span> 和 <span class="codeph"> 視頻 </span> 屬性 <span class="codeph"> EXT-X — 流 — INF </span> 標籤 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK alternate audio </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
