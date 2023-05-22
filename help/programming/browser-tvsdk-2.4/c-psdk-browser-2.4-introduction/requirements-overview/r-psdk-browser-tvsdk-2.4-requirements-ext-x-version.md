---
description: The version of EXT-X-VERSION in the .m3u8 file affects what features are available to your application and what EXT tags are valid in your playlist/manifest.
title: EXT-X-VERSION requirements
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# EXT-X-VERSION requirements{#ext-x-version-requirements}

`#EXT-X-VERSION`

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur. [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)
* Adobe recommends using at least version 2 for playback in Browser TVSDK-based clients.

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
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph"></span> <p><span class="codeph"></span>Version 3 and above require durations to be exact in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"></span> </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph"></span><span class="codeph"></span><span class="codeph"></span> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
