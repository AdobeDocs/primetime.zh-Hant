---
description: TVSDK需要媒體內容、資訊清單內容和軟體版本的特定屬性。
title: 需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# 要求{#requirements}

TVSDK需要媒體內容、資訊清單內容和軟體版本的特定屬性。

## 系統和軟體要求{#section_61C32A0209C44230B392B113B85643EE}

若要使用TVSDK，請確定您的硬體、作業系統和應用程式版本均符合下列最低要求。

作業系統：iOS 6.0或更新版本

## 內容與資訊清單需求{#section_05FA02E2189742008DA09D87E66DCAB7}

檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。

| 內容區段關鍵影格 | 每個內容區段必須以關鍵影格開頭。 |
|---|---|
| 即時／線性視訊中的序號 | 必須在任何指定時間針對主要內容的所有位元速率轉譯之間進行比對。 |

## #EXT-X-VERSION要求{#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

[!DNL .m3u8]檔案中的`#EXT-X-VERSION`版本會影響您應用程式可用的功能，以及`EXT`標籤在播放清單／資訊清單中的有效性。

以下是有關`#EXT-X-VERSION`標籤的一些資訊，該標籤指定HLS協定版本：

* 此版本必須符合HLS播放清單中的功能和屬性；否則，可能會發生播放錯誤。

   如需詳細資訊，請參閱[HTTP即時串流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* 如果標籤未包含在主版或媒體播放清單中，或未指定版本，則預設會使用版本1。 不符合第1版的內容將不會播放。
* Adobe建議至少使用第2版在TVSDK用戶端中播放。

客戶端和伺服器必須以下列方式實施版本：

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 若要使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>標籤的IV屬性。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點<span class="codeph">滅絕FF </span>持續時間值 <p>持續時間標籤(<span class="codeph"> #IFF:版本2中的</span>&lt;duration&gt;,&lt;title&gt;)已四捨五入為整數值。 第3版及以上版本需要在浮動點中精確顯示持續時間。 </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK功能，例如廣告插入和順暢的ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4  </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph"> EXT-X-BYTERANGE </span>標籤 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>標籤 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span>標籤 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2"><span class="codeph"> EXT-X-MEDIA </span>標籤 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34"><span class="codeph"> EXT-X-STREAM-INF </span>標籤的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>屬性 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
