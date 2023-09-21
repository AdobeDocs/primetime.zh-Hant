---
description: 瀏覽器TVSDK支援許多DASH功能，您可實作這些功能，以將功能新增至視訊應用程式。
title: 支援的DASH功能
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 支援的DASH功能{#supported-dash-features}

瀏覽器TVSDK支援許多DASH功能，您可實作這些功能，以將功能新增至視訊應用程式。

* [虛線核心播放功能](#dash-core-playback)
* [DASH進階播放功能](#dash-advanced-playback)
* [DASH內容保護功能](#dash-content-protection)
* [DASH Core廣告插入功能](#dash-core-ad-insertion)
* [DASH進階廣告插入功能](#dash-advanced-insertion-features)
* [DASH整合](#dash-integrations)

>[!TIP]
>
>在下方的功能矩陣表中，  ![](assets/supported15.png)
>表示目前版本支援此功能。

支援下列功能：

<!-- 

<table id="table_lrb_p2g_xx"> 
 <title>DASH integrations</title> 
 <tgroup cols="4"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col6" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" class="entry"> Category </th> 
    <th colname="col2" class="entry"> Content type </th> 
    <th colname="col3" class="entry"> Feature </th> 
    <th colname="col6" align="center" class="entry"> 
     <lines>
       HTML5 FF, IE, Chrome, Android Chrome
     </lines> </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_14D9248BD1D8410E83AD27DB4AB3B6ED" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_EFA853CB763446B3B37F2CF6BCC53EE1" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Billing </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_B3A4E5937CEC4052977C08767219BC2B" /> </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Browserify </td> 
    <td colname="col6" valign="middle" align="center"><img href="assets/supported15.png" id="image_3330E81B86C84AD391AEBFDFE911A47F" /> </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## DASH整合 {#dash-integrations}

| 類別 | 內容型別 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 整合 | VOD +即時 | Adobe Analytics VHL整合 | ![](assets/supported15.png) |
| 整合 | VOD +即時 | 帳單 | ![](assets/supported15.png) |
| 整合 | VOD +即時 | Browserify | ![](assets/supported15.png) |

## DASH進階廣告插入功能(CSAI) {#dash-advanced-insertion-features}

| 類別 | 內容型別 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | 僅限廣告 | 不支援 |
| Ad Insertion | VOD | 目標定位引數 | 僅限VOD |
| Ad Insertion | VOD | 自訂引數 | 僅限VOD |
| Ad Insertion | VOD +即時 | 自訂廣告原則 | 不支援 |
| Ad Insertion | VOD +即時 | 延遲廣告載入 | 不支援 |
| Ad Insertion | VOD | 隨附廣告、橫幅廣告和可點按廣告 | 不支援 |
| Ad Insertion | VOD | VPAID 2.0 | 不支援 |

## DASH核心廣告插入功能(CSAI) {#dash-core-ad-insertion}

| 類別 | 內容型別 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD +即時 | 前置滾動 | 僅限VOD |
| Ad Insertion | VOD +即時 | 中間滾動 | 僅限VOD |
| Ad Insertion | VOD +即時 | 後置滾動 | 僅限VOD |
| Ad Insertion | FER VOD | 廣告解析度和行為 | 不支援 |
| Ad Insertion | VOD +即時 | 預設廣告原則 | 僅限VOD |
| Ad Insertion | VOD +即時 | VAST 2.0/3.0 | 僅限VOD |
| Ad Insertion | VOD +即時 | VMAP 1.0 | 僅限VOD |
| Ad Insertion | VOD +即時 | CRS v3.1 | 僅限VOD |

## DASH內容保護功能 {#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 類別 </th> 
   <th colname="col2" class="entry"> 內容型別 </th> 
   <th colname="col3" class="entry"> 功能 </th> 
   <th colname="col6" class="entry"> HTML5 FF、IE、Chrome、Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD +即時 </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> 不支援 </td>
  </tr> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD +即時 </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> 不支援 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine開啟 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">鉻黃 </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">Windows 8.1和Edge上的Internet Explorer上的PlayReady </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Windows Firefox的Adobe存取（僅限影片） </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 破折號進階播放功能 {#dash-advanced-playback}

| 類別 | 內容型別 | 功能 | HTML5， FF， IE， Chrome， Android Chrome |
|---|---|---|---|
| 播放 | VOD | 在位移處播放 | ![](assets/supported15.png) |
| 播放 | VOD | 僅限音訊的播放 | ![](assets/supported15.png) |
| 播放 | VOD | 特技播放 | ![](assets/supported15.png) |
| 播放 | VOD | Smooth Trick Play | ![](assets/supported15.png) |
| 播放 | VOD +即時 | ID3剖析 | 不支援 |
| 播放 | VOD | 多期間支援 | 僅限VOD |
| 播放 | VOD +即時 | 代碼化的串流 | 不支援 |
| 播放 | VOD +即時 | 帳單 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | Browserify | ![](assets/supported15.png) |

## 虛線核心播放功能 {#dash-core-playback}

| 類別 | 內容型別 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD +即時 | 一般播放（播放、暫停、搜尋） | ![](assets/supported15.png) |
| 播放 | FER VOD | 一般播放（播放、暫停、搜尋） | 不支援 |
| 播放 | VOD +即時 | 最適化位元速率 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | 608/708字幕 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | WebVTT | 僅限VOD |
| 播放 | VOD +即時 | 容錯移轉 | 僅限VOD |
| 播放 | VOD +即時 | QoS和播放器通知 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | 支援Cookie標頭 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | 設定緩衝區控制引數 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | 設定最適化位元速率控制項 | ![](assets/supported15.png) |
| 播放 | VOD +即時 | 自訂標籤(EventStream) | 僅限VOD （內嵌） |
| 播放 | VOD +即時 | 延遲繫結音訊 | 僅限VOD |
| 播放 | VOD +即時 | 302重新導向 | 僅限VOD |
