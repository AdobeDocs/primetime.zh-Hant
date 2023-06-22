---
description: TVSDK has specific requirements for media content, manifest content, DRM, and software versions.
title: Requirements
exl-id: 85bf7b85-5f4b-4ed5-aa4f-765dabc5d4d8
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Requirements {#requirements}

TVSDK has specific requirements for media content, manifest content, DRM, and software versions.

## 系統和軟體需求 {#section_96E5B079900246E78682AE44D3F23068}

若要使用TVSDK，請確認您的硬體、作業系統和應用程式版本均符合下列最低需求。

| 作業系統 | Android 4.0或更新版本（最低API層級14） |
|---|---|
| CPU | 1 GHz單核心或同等規格 |
| RAM | 256 MB |
| GPU | Hardware GPU required for playback |
| Architecture | x86 via Houdini、ARM64、ARMv7和ARMv8 |

## 內容和資訊清單需求 {#section_72DD0E4DA9774DCCADB42887497F1386}

檢查串流和播放清單（資訊清單）的限制和需求，包括DRM加密金鑰。

| Adobe存取DRM | 如果受DRM保護的資料流是多位元速率(MBR)，則用於MBR的DRM加密金鑰應與所有位元速率資料流中使用的金鑰相同。 |
|---|---|
| 廣告變體資訊清單 | Must have the same bit-rate renditions as the renditions of the main content. |

## #EXT-X-VERSION requirements {#section_49A33664651A46EC9ED888BA9C1C3F6D}

`#EXT-X-VERSION`[!DNL .m3u8]`EXT`

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur. 如需詳細資訊，請參閱 [HTTP即時資料流規格](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1).
* Adobe建議至少使用HLS第2版在TVSDK型使用者端中播放。

   使用者端和伺服器必須以下列方式實作版本：

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
   <td colname="2"> 的IV屬性 <span class="codeph"> EXT-X-KEY </span> 標籤之間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784"><span class="codeph"></span> <p><span class="codeph"></span>Version 3 and above require durations to be specified exactly, in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"></span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">此 <span class="codeph"> EXT-X-BYTERANGE </span> 標籤 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">此 <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> 標籤 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">此 <span class="codeph"> 僅限EXT-X-I-FRAMES </span> 標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">此 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">此 <span class="codeph"> 音訊 </span> 和 <span class="codeph"> 視訊 </span> 屬性 <span class="codeph"> EXT-X-STREAM-INF </span> 標籤 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK替代音訊 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
