---
description: TVSDK 需要 媒體 內容、清單內容和軟體版本的特定屬性。
title: 需求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 需求 {#requirements}

TVSDK需要媒體內容、資訊清單內容和軟體版本的特定屬性。

## 系統和軟體需求 {#section_61C32A0209C44230B392B113B85643EE}

要使用 TVSDK，請確保您的硬體、作業系統和應用程式版本都滿足下面列出的最低要求。

作業系統： iOS 6.0 或更高版本

## 內容和清單要求 {#section_05FA02E2189742008DA09D87E66DCAB7}

檢查流和播放清單（清單）的限制和要求，包括 DRM 加密金鑰。

| 關鍵幀區段內容 | 每個內容 區段都必須以關鍵幀開頭。 |
|---|---|
| 即時/線性視訊中的序號 | 在任何指定時間，主要內容的所有位元速率轉譯之間都必須相符。 |

## #EXT-X-VERSION統需求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

的版本 `#EXT-X-VERSION` 在 [!DNL .m3u8] 檔案會影響您的應用程式可以使用哪些功能，以及 `EXT` 標籤在您的播放清單/資訊清單中有效。

下面是有關 `#EXT-X-VERSION` 指定 HLS 協定版本的標記的一些資訊：

* 版本必須與 HLS 播放清單中的功能和屬性匹配;否則，可能會發生播放錯誤。

  有關詳細資訊，請參閱 [ HTTP 即時流式處理規範 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* 如果主播放清單或媒體播放清單中未包含標記，或者未指定版本，則預設使用版本 1。 不符合版本 1 的內容將無法播放。
* Adobe Systems建議至少使用 2 版才能在基於 TVSDK 的用戶端中進行播放。

用戶端和伺服器必須按以下方式實施版本：

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 要使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：2 </span> </td> 
   <td colname="2"> 的IV屬性 <span class="codeph"> EXT-X-KEY </span> 標籤之間。 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點 <span class="codeph"> EXTINF </span> 持續時間值 <p>持續時間標記 （ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;） 在版本 2 中四捨五入為整數值。 &lt;/title&gt;&lt;/duration&gt;版本 3 及更高版本要求持續時間在浮點中精確。 </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK 功能，如廣告插入和無縫 ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION：4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">EXT-X-BYTERANGE <span class="codeph"> </span> 標記 </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">EXT-X-I-FRAME-STREAM-INF <span class="codeph"> </span> 標記 </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK替代音訊 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
