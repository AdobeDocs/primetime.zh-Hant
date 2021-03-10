---
description: 瀏覽器TVSDK支援許多您可實作的HLS功能，以新增功能至視訊應用程式。
title: 支援的HLS功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# 支援的HLS功能{#supported-hls-features}

瀏覽器TVSDK支援許多您可實作的HLS功能，以新增功能至視訊應用程式。

* [HLS Core播放](#hls-core-playback)
* [HLS Advanced Playback功能](#hls-advanced-playback)
* [HLS內容保護功能](#hls-content-protection)
* [HLS核心廣告插入功能](#hls-core-ad-insertion)
* [HLS進階廣告插入功能](#hls-advanced-ad-insertion)
* [HLS整合](#hls-integrations)

>[!TIP]
>
>在以下的功能表格中，![支援的圖示](assets/supported15.png)表示目前版本支援此功能。

>[!TIP]
>
>在Safari欄「平台限制」中，表示不支援使用案例，因為該平台不允許實作支援。 如果是插入，請使用SSAI。 如果您有重要的播放限制，請強制回退至SafariFlash，直到平台支援廣告插入使用案例為止。

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

## HLS整合{#hls-integrations}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 整合 | VOD + Live | Adobe AnalyticsVHL整合 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS進階廣告插入功能(CSAI){#hls-advanced-ad-insertion}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD | 僅限廣告 | 不支援 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD + Live | 定位參數 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD + Live | 自訂廣告原則 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 延遲廣告載入 | ![支援的圖示](assets/supported15.png) | 不支援 | 平台限制 |
| Ad Insertion | VOD | 配套廣告、橫幅廣告和可點選廣告 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD | VPAID 2.0 | SWF | JavaScript | JavaScript |

## HLS核心廣告插入功能(CSAI){#hls-core-ad-insertion}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Live | 前滾 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD + Live | 中間卷 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 後置卷 | 僅限VOD | 僅限VOD | 僅限VOD |
| Ad Insertion | FER VOD | 廣告解析度與行為 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 預設廣告原則 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | VAST 2.0/3.0 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD + Live | VMAP 1.0 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| Ad Insertion | VOD + Live | CRS v3.1 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS內容保護功能{#hls-content-protection}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 內容保護 | VOD + Live | AES-128 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 內容保護 | VOD + Live | Sample-AES | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 內容保護 | VOD | DRM | Adobe存取 | 不支援 | FairPlay |

## HLS高級回放功能{#hls-advanced-playback}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD | 在偏移處播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 僅限音訊播放 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 特技遊戲 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD | 流暢的戲法遊戲 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | ID3剖析 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 不支援 |
| 播放 | VOD + Live | 不連續標籤支援 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | Token化串流 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 帳單 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | 瀏覽 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |

## HLS核心播放{#hls-core-playback}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD + Live | 一般播放（播放、暫停、搜尋） | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | FER VOD | 一般播放（播放、暫停、搜尋） | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | 自適應位元速率 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | 608/708標題 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | WebVTT | ![支援的圖示](assets/supported15.png) | 僅限VOD | 僅限VOD |
| 播放 | VOD + Live | 資訊清單容錯移轉 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) |
| 播放 | VOD + Live | 高級故障切換 | ![支援的圖示](assets/supported15.png) | 僅限VOD | 平台限制 |
| 播放 | VOD + Live | QoS和播放器通知 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 有限的QoS支援 |
| 播放 | VOD + Live | 支援Cookie標題 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 設定緩衝器控制參數 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 設定自適應位元速率控制 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 自訂標籤 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 延遲裝訂音訊 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 302重新導向 | ![支援的圖示](assets/supported15.png) | ![支援的圖示](assets/supported15.png) | 平台限制 |