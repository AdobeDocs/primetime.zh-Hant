---
description: TVSDK 對媒體 內容、清單內容、DRM 和軟體版本有特定要求。
title: 需求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 需求 {#requirements}

TVSDK需要媒體內容、資訊清單內容、DRM和軟體版本的特定屬性。

## 系統和軟體需求 {#section_96E5B079900246E78682AE44D3F23068}

要使用 TVSDK，請確保您的硬體、作業系統和應用程式版本都滿足下面列出的最低要求。

| 作業系統 | iOS 7.0 或更高版本 |
|---|---|
| Xcode | Xcode 10 for iOS 12 和 Xcode 9 for iOS 11 |

## 內容和清單要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

檢查串流和播放清單（資訊清單）的限制和需求，包括DRM加密金鑰。

| 內容區段關鍵影格 | 每個內容區段都必須以關鍵框架開頭。 |
|---|---|
| 即時/線性視訊中的序號 | 在任何給定時間，主內容的所有位元速率演繹版必須匹配。 |

## EXT-X-VERSION 要求 {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

清單檔中的版本 `#EXT-X-VERSION` [!DNL .m3u8] 會影響哪些功能可供您的應用程式以及哪些 `EXT` 標記有效。

下面是有關 `#EXT-X-VERSION` 指定 HLS 協定版本的標記的一些資訊：

* 版本必須與 HLS 播放清單中的功能和屬性匹配;否則，可能會發生播放錯誤。 有關詳細資訊，請參閱 [ HTTP 即時流式處理規範 ](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1) 。
* Adobe Systems建議至少使用 版本 2 個 HLS 在基於 TVSDK 的用戶端中進行播放。

  用戶端和伺服器必須按以下方式實施版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 若要使用這些功能 </th> 
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
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點 <span class="codeph"> EXTINF </span> 持續時間值 <p>持續時間標記 （ <span class="codeph"> #EXTINF： </span>&lt;duration&gt;,&lt;title&gt;） 在版本 2 中四捨五入為整數值。 &lt;/title&gt;&lt;/duration&gt;版本 3 及更高版本要求在浮點數中準確指定持續時間。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION：4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">EXT-X-BYTERANGE <span class="codeph"> </span> 標記 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">EXT-X-I-FRAME-STREAM-INF <span class="codeph"> </span> 標記 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK替代音訊 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
