---
description: TVSDK has specific requirements for media content, manifest content, DRM, and software versions.
title: 要求
exl-id: 8c611ad4-ad04-4bab-83b9-0d8fb6c5cf3d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 要求 {#requirements}

TVSDK需要媒體內容、清單內容、DRM和軟體版本的特定屬性。

## System and software requirements {#section_96E5B079900246E78682AE44D3F23068}

To use TVSDK, ensure that your hardware, operating system, and application versions all meet the minimum requirements listed below.

| Operating system | iOS 7.0 or later |
|---|---|
| Xcode | Xcode 10 for iOS 12 and Xcode 9 for iOS 11 |

## Content and manifest requirements {#section_72DD0E4DA9774DCCADB42887497F1386}

檢查流和播放清單（清單）（包括DRM加密密鑰）的限制和要求。

| 內容段關鍵幀 | 每個內容段必須以關鍵幀開頭。 |
|---|---|
| 即時/線性視頻中的序列號 | Must match between all bit-rate renditions for the main content at any given time. |

## EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

`#EXT-X-VERSION`[!DNL .m3u8]`EXT`

`#EXT-X-VERSION`

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur. [](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1)
* Adobe recommends using at least Version 2 of HLS for playback in TVSDK-based clients.

   Clients and servers must implement the versions in the following way:

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Use at least this version </th> 
   <th colname="2" class="entry"> 使用這些功能 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X — 版本：2 </span> </td> 
   <td colname="2"> <span class="codeph"></span> </td> 
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
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350"><span class="codeph"></span> </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287"><span class="codeph"></span> </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">的 <span class="codeph"> 僅EXT-X-I — 幀 </span> 標籤 </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">的 <span class="codeph"> EXT-X-MEDIA </span> 標籤 </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">的 <span class="codeph"> 音頻 </span> 和 <span class="codeph"> 視頻 </span> 屬性 <span class="codeph"> EXT-X — 流 — INF </span> 標籤 </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK備用音頻 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
