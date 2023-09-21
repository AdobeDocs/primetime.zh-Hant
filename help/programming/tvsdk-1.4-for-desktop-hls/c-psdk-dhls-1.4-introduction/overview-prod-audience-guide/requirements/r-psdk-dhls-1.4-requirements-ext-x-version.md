---
description: .m3u8 檔中的 EXT-X-VERSION 版本會影響應用程式可用的功能以及播放清單/清單中哪些 EXT 標記有效。
title: EXT-X-VERSION 要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# EXT-X-VERSION 要求{#ext-x-version-requirements}

.m3u8 檔中的 #EXT-X-VERSION 版本會影響應用程式可用的功能以及播放清單/清單中有效的 EXT 標記。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

下面是有關 `#EXT-X-VERSION` 指定 HLS 協定版本的標記的一些資訊：

* 版本必須與 HLS 播放清單中的功能和屬性匹配;否則，可能會發生播放錯誤。

  有關詳細資訊，請參閱 [ HTTP 即時流式處理規範 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* 版本必須與 HLS 播放清單中的功能和屬性匹配;否則，可能會發生播放錯誤。

  有關詳細資訊，請參閱 [ HTTP 即時流式處理規範 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* Adobe Systems建議至少使用版本 2 在基於的用戶端中進行播放。

  用戶端和伺服器必須按以下方式實施版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> EXT-X-KEY </span> 標記的 <span class="codeph"> IV 屬性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點 <span class="codeph"> EXTINF </span> 持續時間值 <p>持續時間標記 （ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;） 在版本 2 中四捨五入為整數值。 &lt;/title&gt;&lt;/duration&gt;版本 3 及更高版本要求持續時間在浮點中精確。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION：4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">EXT-X-BYTERANGE <span class="codeph"> </span> 標記 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">EXT-X-I-FRAME-STREAM-INF <span class="codeph"> </span> 標記 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">EXT-X-I-FRAMES-ONLY <span class="codeph"> </span> 標記 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph">EXT-X-MEDIA </span> 標記 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK 替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
