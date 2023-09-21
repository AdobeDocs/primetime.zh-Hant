---
description: 瀏覽器TVSDK支援許多HLS功能，您可實作以新增功能至視訊應用程式。
title: 支援的HLS功能
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 支援的HLS功能 {#supported-hls-features}

瀏覽器TVSDK支援許多HLS功能，您可實作以新增功能至視訊應用程式。

* [HLS核心播放](#hls-core-playback)
* [HLS進階播放功能](#hls-advanced-playback)
* [HLS內容保護功能](#hls-content-protection)
* [HLS核心廣告插入功能](#hls-core-ad-insertion)
* [HLS進階廣告插入功能](#hls-advanced-ad-insertion)
* [HLS整合](#hls-integrations)

>[!TIP]
>
>在下方的功能矩陣表中， ![支援的圖示](assets/supported15.png) 表示目前版本支援此功能。

>[!TIP]
>
>在Safari欄中，「平台限制」表示該使用案例不受支援，因為該平台不允許實作對其的支援。 如果是插入，請使用SSAI。 如果您有重要的播放限制，請強制在Safari上遞補Flash，直到平台支援廣告插入使用案例為止。

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

支援下列功能：

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## HLS整合 {#hls-integrations}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 整合 | VOD +即時 | Adobe Analytics VHL整合 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS進階廣告插入功能(CSAI) {#hls-advanced-ad-insertion}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | 僅限廣告 | 不支援 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD +即時 | 目標定位引數 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD +即時 | 自訂廣告原則 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +即時 | 延遲廣告載入 | ![支援的圖示](assets/supported15.png) | 不支援 | 平台限制 |
| Ad Insertion | VOD | 隨附廣告、橫幅廣告和可點按廣告 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## HLS核心廣告插入功能(CSAI) {#hls-core-ad-insertion}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD +即時 | 前置滾動 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD +即時 | 中間滾動 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +即時 | 後置滾動 | 僅限VOD | 僅限VOD | 僅限VOD |
| Ad Insertion | FER VOD | 廣告解析度和行為 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +即時 | 預設廣告原則 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD +即時 | VAST 2.0/3.0 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD +即時 | VMAP 1.0 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD +即時 | CRS v3.1 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS內容保護功能 {#hls-content-protection}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 內容保護 | VOD +即時 | AES-128 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 內容保護 | VOD +即時 | Sample-AES | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 內容保護 | VOD | DRM | Adobe存取 | 不支援 | FairPlay |

## HLS進階播放功能 {#hls-advanced-playback}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD | 在位移處播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 僅限音訊的播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 特技播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 平滑特技播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | ID3剖析 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 不支援 |
| 播放 | VOD +即時 | 支援不連續標籤 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | 代碼化的串流 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 帳單 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | Browserify | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS核心播放 {#hls-core-playback}

| 類別 | 內容型別 | 功能 | Flash | HTML5：FF、IE、Chrome、Android Chrome | HTML5：Safari、iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD +即時 | 一般播放（播放、暫停、搜尋） | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | FER VOD | 一般播放（播放、暫停、搜尋） | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | 最適化位元速率 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | 608/708字幕 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | WebVTT | ![支援的圖示](assets/supported15.png) | 僅限VOD | 僅限VOD |
| 播放 | VOD +即時 | 資訊清單容錯移轉 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD +即時 | 進階容錯移轉 | ![支援的圖示](assets/supported15.png) | 僅限VOD | 平台限制 |
| 播放 | VOD +即時 | QoS和播放器通知 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 有限的QoS支援 |
| 播放 | VOD +即時 | 支援Cookie標頭 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 設定緩衝區控制引數 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 設定最適化位元速率控制項 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 自訂標籤 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 延遲繫結音訊 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD +即時 | 302重新導向 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
