---
description: .m3u8檔案中的#EXT-X-VERSION版本會影響您應用程式可用的功能，以及播放清單／資訊清單中有效的EXT標籤。
seo-description: .m3u8檔案中的#EXT-X-VERSION版本會影響您應用程式可用的功能，以及播放清單／資訊清單中有效的EXT標籤。
seo-title: '#EXT-X-VERSION需求'
title: '#EXT-X-VERSION需求'
uuid: c862df4a-88ba-4497-8b7c-b83fcb34b8bb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# #EXT-X-VERSION需求{#ext-x-version-requirements}

.m3u8檔案中的#EXT-X-VERSION版本會影響您應用程式可用的功能，以及播放清單／資訊清單中有效的EXT標籤。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有關標籤的一 `#EXT-X-VERSION` 些資訊，它指定HLS協定版本：

* 此版本必須符合HLS播放清單中的功能和屬性；否則，可能會發生播放錯誤。

   如需詳細資訊，請參 [閱HTTP即時串流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 此版本必須符合HLS播放清單中的功能和屬性；否則，可能會發生播放錯誤。

   如需詳細資訊，請參 [閱HTTP即時串流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建議至少使用第2版在基於用戶端中播放。

   客戶端和伺服器必須以下列方式實施版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 若要使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> EXT-X-KEY標 <span class="codeph"> 簽的IV屬 </span> 性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點 <span class="codeph"> DIVAF持 </span> 續時間值 <p>持續時間標籤( <span class="codeph"> #DIVAF:版 </span>本2中的&lt;duration&gt;,&lt;title&gt;)已四捨五入為整數值。 第3版及以上版本需要在浮動點中精確顯示持續時間。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">EXT- <span class="codeph"> X-BYTERANGE標 </span> 記 </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF標 </span> 簽 </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">僅 <span class="codeph"> 限EXT-X-I-FRAMES標 </span> 簽 </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB"><span class="codeph"> EXT-X-MEDIA標 </span> 簽 </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">EXT-X- <span class="codeph"> STREAM-INF標 </span> 簽的音 <span class="codeph"> 訊和視訊屬 </span><span class="codeph"></span> 性 </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

