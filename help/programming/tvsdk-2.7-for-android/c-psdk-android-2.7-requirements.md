---
description: TVSDK has specific requirements for media content, manifest content, DRM, and software versions.
title: Requirements
exl-id: 8c252761-eee3-4fec-a85f-a38c1d9be9cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Requirements {#requirements}

TVSDK has specific requirements for media content, manifest content, DRM, and software versions.

## 系統和軟體要求 {#section_96E5B079900246E78682AE44D3F23068}

要使用TVSDK，請確保您的硬體、作業系統和應用程式版本都符合下面列出的最低要求。

| 作業系統 | Android 4.0或更高版本（最低API級別14） |
|---|---|
| CPU | 1 GHz單核或等效 |
| RAM | 256 MB |
| GPU | Hardware GPU required for playback |
| Architecture | x86，通過Houdini、ARM64、ARMv7和ARMv8 |

## 內容和清單要求 {#section_72DD0E4DA9774DCCADB42887497F1386}

檢查流和播放清單（清單）（包括DRM加密密鑰）的限制和要求。

| Adobe訪問DRM | 如果受DRM保護的流是多比特率(MBR)，則用於MBR的DRM加密密鑰應與所有比特率流中使用的密鑰相同。 |
|---|---|
| 廣告變型清單 | Must have the same bit-rate renditions as the renditions of the main content. |

## #EXT-X-VERSION requirements {#section_49A33664651A46EC9ED888BA9C1C3F6D}

`#EXT-X-VERSION`[!DNL .m3u8]`EXT`

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur. 有關詳細資訊，請參見 [HTTP即時流規範](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)。
* Adobe建議至少使用HLS第2版在基於TVSDK的客戶端中回放。

   客戶端和伺服器必須通過以下方式實現版本：

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 至少使用此版本 </th> 
   <th colname="2" class="entry"> 使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X — 版本：2 </span> </td> 
   <td colname="2"> IV屬性 <span class="codeph"> EXT-X鍵 </span> 標籤。 </td> 
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
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">的 <span class="codeph"> EXT-X-BYTERANGE </span> 標籤 </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">的 <span class="codeph"> EXT-X-I — 幀 — 流 — INF </span> 標籤 </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">的 <span class="codeph"> 僅EXT-X-I — 幀 </span> 標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">的 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">的 <span class="codeph"> 音頻 </span> 和 <span class="codeph"> 視頻 </span> 屬性 <span class="codeph"> EXT-X — 流 — INF </span> 標籤 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK備用音頻 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
