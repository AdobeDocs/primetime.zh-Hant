---
description: 瀏覽器TVSDK支援許多HLS功能，您可以實施這些功能來向視頻應用程式添加功能。
title: 支援的HLS功能
exl-id: 111a6683-fb5c-4f0a-8665-5b1aab77056c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 支援的HLS功能 {#supported-hls-features}

瀏覽器TVSDK支援許多HLS功能，您可以實施這些功能來向視頻應用程式添加功能。

* [HLS核心播放](#hls-core-playback)
* [HLS高級回放功能](#hls-advanced-playback)
* [HLS內容保護功能](#hls-content-protection)
* [HLS核心和插入功能](#hls-core-ad-insertion)
* [HLS高級和插入功能](#hls-advanced-ad-insertion)
* [HLS整合](#hls-integrations)

>[!TIP]
>
>在下面的特徵矩陣表中， ![支援的表徵圖](assets/supported15.png) 表示在當前版本中支援該功能。

>[!TIP]
>
>在Safari列「平台限制」中，表示不支援使用案例，因為該平台不允許實現對它的支援。 在插入時，使用SSAI。 如果播放限制對您很重要，則強制回退到Safari上的Flash，直到平台支援廣告插入使用案例。

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

支援以下功能：

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

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 整合 | VOD + Live | Adobe AnalyticsVHL整合 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |

## HLS高級和插入功能(CSAI) {#hls-advanced-ad-insertion}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | 視頻點播 | 僅廣告 | 不支援 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | VOD + Live | 目標參數 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | VOD + Live | 自定義廣告策略 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 懶惰載入 | ![支援的表徵圖](assets/supported15.png) | 不支援 | 平台限制 |
| Ad Insertion | 視頻點播 | 伴侶廣告、橫幅廣告和可點擊廣告 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | 視頻點播 | VPAID 2.0 | SWF | JavaScript | JavaScript |

## HLS核心和插入功能(CSAI) {#hls-core-ad-insertion}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| Ad Insertion | VOD + Live | 預卷 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | VOD + Live | 中間卷 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 後滾 | 僅VOD | 僅VOD | 僅VOD |
| Ad Insertion | FER視頻點播 | 廣告解析度和行為 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 預設廣告策略 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| Ad Insertion | VOD + Live | 廣2.0/3.0 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | VOD + Live | VMAP 1.0 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| Ad Insertion | VOD + Live | CRS 3.1版 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |

## HLS內容保護功能 {#hls-content-protection}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 內容保護 | VOD + Live | AES-128 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 內容保護 | VOD + Live | 樣本 — AES | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 內容保護 | 視頻點播 | DRM | Adobe訪問 | 不支援 | 公平遊戲 |

## HLS高級回放功能 {#hls-advanced-playback}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 播放 | 視頻點播 | 偏移處回放 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | 視頻點播 | 僅播放音頻 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | 視頻點播 | 戲法 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | 視頻點播 | 平滑戲法 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | ID3分析 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 不支援 |
| 播放 | VOD + Live | 不連續標籤支援 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | 標籤化流 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 計費 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | 瀏覽 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |

## HLS核心回放 {#hls-core-playback}

| 類別 | 內容類型 | 功能 | Flash | HTML5:FF、IE、Chrome、Android Chrome | HTML5:薩法里，iOS |
|--- |--- |--- |--- |--- |--- |
| 播放 | VOD + Live | 常規播放（播放、暫停、查找） | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | FER視頻點播 | 常規播放（播放、暫停、查找） | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | 自適應比特率 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | 608/708字幕 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | WebVTT | ![支援的表徵圖](assets/supported15.png) | 僅VOD | 僅VOD |
| 播放 | VOD + Live | 清單故障轉移 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) |
| 播放 | VOD + Live | 高級故障切換 | ![支援的表徵圖](assets/supported15.png) | 僅VOD | 平台限制 |
| 播放 | VOD + Live | QoS和播放器通知 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 有限的QoS支援 |
| 播放 | VOD + Live | 支援Cookie標頭 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 設定緩衝區控制參數 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 設定自適應比特率控制 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 自定義標籤 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 延遲綁定音頻 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
| 播放 | VOD + Live | 302重定向 | ![支援的表徵圖](assets/supported15.png) | ![支援的表徵圖](assets/supported15.png) | 平台限制 |
