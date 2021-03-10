---
description: TVSDK對媒體內容、資訊清單內容、DRM和軟體版本有特定需求。
title: 需求
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# 要求{#requirements}

TVSDK需要媒體內容、資訊清單內容、DRM和軟體版本的特定屬性。

## 系統和軟體要求{#section_96E5B079900246E78682AE44D3F23068}

若要使用TVSDK，請確定您的硬體、作業系統和應用程式版本均符合下列最低要求。

| 作業系統 | iOS 7.0或更新版本 |
|---|---|
| Xcode | iOS 12適用的Xcode 10和iOS 11適用的Xcode 9 |

## 內容與資訊清單需求{#section_72DD0E4DA9774DCCADB42887497F1386}

檢查串流和播放清單（清單）的限制和要求，包括DRM加密金鑰。

| 內容區段關鍵影格 | 每個內容區段必須以關鍵影格開頭。 |
|---|---|
| 即時／線性視訊中的序號 | 必須在任何指定時間針對主要內容的所有位元速率轉譯之間進行比對。 |

## EXT-X-VERSION要求{#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

[!DNL .m3u8]資訊清單檔案中的`#EXT-X-VERSION`版本會影響您的應用程式有哪些可用功能，以及哪些`EXT`標籤有效。

以下是有關`#EXT-X-VERSION`標籤的一些資訊，該標籤指定HLS協定版本：

* 此版本必須符合HLS播放清單中的功能和屬性；否則，可能會發生播放錯誤。 如需詳細資訊，請參閱[HTTP即時串流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建議至少使用HLS第2版在TVSDK用戶端中播放。

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
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2  </span> </td> 
   <td colname="2"> <span class="codeph"> EXT-X-KEY </span>標籤的IV屬性。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3  </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">浮點<span class="codeph">滅絕FF </span>持續時間值 <p>持續時間標籤(<span class="codeph"> #IFF:版本2中的</span>&lt;duration&gt;,&lt;title&gt;)已四捨五入為整數值。 第3版及以上版本需要精確指定浮點數的持續時間。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4  </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350"><span class="codeph"> EXT-X-BYTERANGE </span>標籤 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287"><span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span>標籤 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9"><span class="codeph"> EXT-X-I-FRAMES-ONLY </span>標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B"><span class="codeph"> EXT-X-MEDIA </span>標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD"><span class="codeph"> EXT-X-STREAM-INF </span>標籤的<span class="codeph"> AUDIO </span>和<span class="codeph"> VIDEO </span>屬性 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK替代音訊 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>