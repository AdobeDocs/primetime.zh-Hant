---
description: .m3u8檔案中的EXT-X-VERSION版本會影響應用程式可用的功能，以及播放清單/資訊清單中有效的EXT標籤。
title: EXT-X-VERSION需求
exl-id: 1b7c205b-c6b1-416f-885a-d1cd23d8e803
source-git-commit: e2a796dc5eb017929297d127cc79b65ba51a0c75
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# EXT-X-VERSION需求{#ext-x-version-requirements}

.m3u8檔案中的`#EXT-X-VERSION`版本會影響應用程式可用的功能，以及播放清單/資訊清單中有效的EXT標籤。

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

以下是有關`#EXT-X-VERSION`標籤的一些資訊，該標籤指定HLS協定版本：

* 版本必須符合HLS播放清單中的功能和屬性；否則，可能會發生播放錯誤。 如需詳細資訊，請參閱[HTTP即時串流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建議在瀏覽器TVSDK型用戶端中使用至少第2版進行播放。

   用戶端和伺服器必須透過下列方式實作版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點<span class="codeph"> OVIFA </span>持續時間值 <p>持續時間標籤(<span class="codeph"> #EXTINF:第2版中的</span>&lt;duration&gt;,&lt;title&gt;)會四捨五入為整數值。 第3版及更高版本要求在浮點中準確顯示持續時間。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA </span>標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph"> EXT-X-STREAM-INF </span>標籤的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>屬性 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
