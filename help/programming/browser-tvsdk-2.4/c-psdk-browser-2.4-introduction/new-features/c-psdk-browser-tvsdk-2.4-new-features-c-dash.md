---
description: 瀏覽器TVSDK支援許多DASH功能，您可實作這些功能，以新增功能至視訊應用程式。
title: 支援的DASH功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---


# 支援的DASH功能{#supported-dash-features}

瀏覽器TVSDK支援許多DASH功能，您可實作這些功能，以新增功能至視訊應用程式。

* [DASH核心播放功能](#dash-core-playback)
* [DASH進階播放功能](#dash-advanced-playback)
* [DASH內容保護功能](#dash-content-protection)
* [DASH核心廣告插入功能](#dash-core-ad-insertion)
* [DASH進階廣告插入功能](#dash-advanced-insertion-features)
* [DASH整合](#dash-integrations)

>[!TIP]
>
>在下面的功能矩陣表中， ![](assets/supported15.png)
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

## DASH整合{#dash-integrations}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 整合 | VOD + Live | Adobe AnalyticsVHL整合 | ![](assets/supported15.png) |
| 整合 | VOD + Live | 帳單 | ![](assets/supported15.png) |
| 整合 | VOD + Live | 瀏覽 | ![](assets/supported15.png) |

## DASH進階廣告插入功能(CSAI){#dash-advanced-insertion-features}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD | 僅限廣告 | 不支援 |
| Ad Insertion | VOD | 定位參數 | 僅限VOD |
| Ad Insertion | VOD | 自訂參數 | 僅限VOD |
| Ad Insertion | VOD + Live | 自訂廣告原則 | 不支援 |
| Ad Insertion | VOD + Live | 延遲廣告載入 | 不支援 |
| Ad Insertion | VOD | 配套廣告、橫幅廣告和可點選廣告 | 不支援 |
| Ad Insertion | VOD | VPAID 2.0 | 不支援 |

## DASH核心廣告插入功能(CSAI){#dash-core-ad-insertion}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Live | 前滾 | 僅限VOD |
| Ad Insertion | VOD + Live | 中間卷 | 僅限VOD |
| Ad Insertion | VOD + Live | 後置卷 | 僅限VOD |
| Ad Insertion | FER VOD | 廣告解析度與行為 | 不支援 |
| Ad Insertion | VOD + Live | 預設廣告原則 | 僅限VOD |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | 僅限VOD |
| Ad Insertion | VOD + Live | VMAP 1.0 | 僅限VOD |
| Ad Insertion | VOD + Live | CRS v3.1 | 僅限VOD |

## DASH內容保護功能{#dash-content-protection}

<table id="table_hrb_p2g_xx">  
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 類別 </th> 
   <th colname="col2" class="entry"> 內容類型 </th> 
   <th colname="col3" class="entry"> 功能 </th> 
   <th colname="col6" class="entry"> HTML5 FF、IE、Chrome、Android Chrome</th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> AES-128 </td> 
   <td colname="col6"> 不支援 </td>
  </tr> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD + Live </td> 
   <td colname="col3"> Sample-AES </td> 
   <td colname="col6"> 不支援 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> VOD </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine on 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">Chrome </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">Firefox 47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">Chromecast </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">在Windows 8.1和Edge的Internet Explorer上播放就緒 </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Windows Firefox的Adobe存取（僅限視訊） </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## DASH進階播放功能{#dash-advanced-playback}

| 類別 | 內容類型 | 功能 | HTML5、FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD | 在偏移處播放 | ![](assets/supported15.png) |
| 播放 | VOD | 純音效播放 | ![](assets/supported15.png) |
| 播放 | VOD | 特技遊戲 | ![](assets/supported15.png) |
| 播放 | VOD | 流暢的特技播放 | ![](assets/supported15.png) |
| 播放 | VOD + Live | ID3剖析 | 不支援 |
| 播放 | VOD | 多期支援 | 僅限VOD |
| 播放 | VOD + Live | Token化串流 | 不支援 |
| 播放 | VOD + Live | 帳單 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 瀏覽 | ![](assets/supported15.png) |

## DASH核心播放功能{#dash-core-playback}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD + Live | 一般播放（播放、暫停、搜尋） | ![](assets/supported15.png) |
| 播放 | FER VOD | 一般播放（播放、暫停、搜尋） | 不支援 |
| 播放 | VOD + Live | 自適應位元速率 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 608/708標題 | ![](assets/supported15.png) |
| 播放 | VOD + Live | WebVTT | 僅限VOD |
| 播放 | VOD + Live | 故障切換 | 僅限VOD |
| 播放 | VOD + Live | QoS和播放器通知 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 支援Cookie標題 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 設定緩衝器控制參數 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 設定自適應位元速率控制 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 自訂標籤(EventStream) | 僅限VOD（內嵌） |
| 播放 | VOD + Live | 延遲裝訂音訊 | 僅限VOD |
| 播放 | VOD + Live | 302重新導向 | 僅限VOD |