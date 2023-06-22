---
description: TVSDK requires specific properties for media content, manifest content, and software versions.
title: 需求
exl-id: 2b81ae19-7907-4038-80e1-f579a8c04540
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 需求 {#requirements}

TVSDK需要媒體內容、資訊清單內容和軟體版本的特定屬性。

## System and software requirements {#section_61C32A0209C44230B392B113B85643EE}

To use TVSDK, ensure that your hardware, operating system, and application versions all meet the minimum requirements listed below.

Operating system: iOS 6.0 or later

## Content and manifest requirements {#section_05FA02E2189742008DA09D87E66DCAB7}

Check the restrictions and requirements for streams and playlists (manifests), including DRM encryption keys.

| Content segment key frames | Each content segment must begin with a key frame. |
|---|---|
| 即時/線性視訊中的序號 | 在任何指定時間，主要內容的所有位元速率轉譯之間都必須相符。 |

## #EXT-X-VERSION統需求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

的版本 `#EXT-X-VERSION` 在 [!DNL .m3u8] 檔案會影響您的應用程式可使用哪些功能，以及 `EXT` 標籤在您的播放清單/資訊清單中有效。

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

   [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)
* If the tag is not included in the master or media playlists, or if no version is specified, version 1 is used by default. Content that does not comply with version 1 will not play.
* Adobe recommends using at least version 2 for playback in TVSDK-based clients.

Clients and servers must implement the versions in the following way:

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Use at least this version </th> 
   <th colname="2" class="entry"> To use these features </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> 的IV屬性 <span class="codeph"> EXT-X-KEY </span> 標籤之間。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph"></span> <p><span class="codeph"></span>Version 3 and above require durations to be exact in floating point. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK features such as ad insertion and seamless ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"></span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927"><span class="codeph"></span> </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF"><span class="codeph"></span> </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
