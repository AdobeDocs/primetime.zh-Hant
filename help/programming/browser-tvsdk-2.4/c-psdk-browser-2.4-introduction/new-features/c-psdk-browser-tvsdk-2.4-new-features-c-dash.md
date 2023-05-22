---
description: 瀏覽器TVSDK支援多種DASH功能，您可以實施這些功能來向視頻應用程式添加功能。
title: 支援的DASH功能
exl-id: 29a5d1a3-e31e-459c-90b5-80227df46e4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# 支援的DASH功能{#supported-dash-features}

瀏覽器TVSDK支援多種DASH功能，您可以實施這些功能來向視頻應用程式添加功能。

* [DASH核心播放功能](#dash-core-playback)
* [DASH高級回放功能](#dash-advanced-playback)
* [DASH內容保護功能](#dash-content-protection)
* [DASH核心和插入功能](#dash-core-ad-insertion)
* [DASH高級廣告插入功能](#dash-advanced-insertion-features)
* [DASH整合](#dash-integrations)

>[!TIP]
>
>在下面的特徵矩陣表中，  ![](assets/supported15.png)
>表示在當前版本中支援該功能。

支援以下功能：

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

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 整合 | VOD + Live | Adobe AnalyticsVHL整合 | ![](assets/supported15.png) |
| 整合 | VOD + Live | 計費 | ![](assets/supported15.png) |
| 整合 | VOD + Live | 瀏覽 | ![](assets/supported15.png) |

## DASH高級和插入功能(CSAI) {#dash-advanced-insertion-features}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | 視頻點播 | 僅廣告 | 不支援 |
| Ad Insertion | 視頻點播 | 目標參數 | 僅VOD |
| Ad Insertion | 視頻點播 | 自定義參數 | 僅VOD |
| Ad Insertion | VOD + Live | 自定義廣告策略 | 不支援 |
| Ad Insertion | VOD + Live | 懶惰載入 | 不支援 |
| Ad Insertion | 視頻點播 | 伴侶廣告、橫幅廣告和可點擊廣告 | 不支援 |
| Ad Insertion | 視頻點播 | VPAID 2.0 | 不支援 |

## DASH核心和插入功能(CSAI) {#dash-core-ad-insertion}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| Ad Insertion | VOD + Live | 預卷 | 僅VOD |
| Ad Insertion | VOD + Live | 中間卷 | 僅VOD |
| Ad Insertion | VOD + Live | 後滾 | 僅VOD |
| Ad Insertion | FER視頻點播 | 廣告解析度和行為 | 不支援 |
| Ad Insertion | VOD + Live | 預設廣告策略 | 僅VOD |
| Ad Insertion | VOD + Live | 廣2.0/3.0 | 僅VOD |
| Ad Insertion | VOD + Live | VMAP 1.0 | 僅VOD |
| Ad Insertion | VOD + Live | CRS 3.1版 | 僅VOD |

## DASH內容保護功能 {#dash-content-protection}

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
   <td colname="col3"> 樣本 — AES </td> 
   <td colname="col6"> 不支援 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 內容保護 </td> 
   <td colname="col2"> 視頻點播 </td> 
   <td colname="col3"> DRM </td> 
   <td colname="col6"> 
    <ul id="ul_irb_p2g_xx"> 
     <li id="li_C4643F2978BC4C8ABDB3E6C72C75A468">Widevine開啟 
      <ul id="ul_7047EA49AA3F40FE8F90E0ED6C028D83"> 
       <li id="li_B575735388D74D789D56BF373A470A6D">鉻 </li> 
       <li id="li_855146E4AC3A48E69B65F0022E1C0156">火狐47+ </li> 
       <li id="li_BC06B0A6EAAC4FC991C713775A8BB4DA">色甲司特 </li> 
      </ul> </li> 
     <li id="li_D48B51C2208F423CB85D08886C2E1C66">在Windows 8.1和Edge上的Internet Explorer上播放PlayReady </li> 
     <li id="li_2786AC19387241A296E015EE6FD07F2D">Adobe訪問Windows Firefox（僅限視頻） </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## DASH高級回放功能 {#dash-advanced-playback}

| 類別 | 內容類型 | 功能 | HTML5、FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | 視頻點播 | 偏移處回放 | ![](assets/supported15.png) |
| 播放 | 視頻點播 | 僅音頻播放 | ![](assets/supported15.png) |
| 播放 | 視頻點播 | 戲法 | ![](assets/supported15.png) |
| 播放 | 視頻點播 | 平滑特技遊戲 | ![](assets/supported15.png) |
| 播放 | VOD + Live | ID3分析 | 不支援 |
| 播放 | 視頻點播 | 多期支助 | 僅VOD |
| 播放 | VOD + Live | 標籤化流 | 不支援 |
| 播放 | VOD + Live | 計費 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 瀏覽 | ![](assets/supported15.png) |

## DASH核心播放功能 {#dash-core-playback}

| 類別 | 內容類型 | 功能 | HTML5 FF、IE、Chrome、Android Chrome |
|---|---|---|---|
| 播放 | VOD + Live | 常規播放（播放、暫停、查找） | ![](assets/supported15.png) |
| 播放 | FER視頻點播 | 常規播放（播放、暫停、查找） | 不支援 |
| 播放 | VOD + Live | 自適應比特率 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 608/708字幕 | ![](assets/supported15.png) |
| 播放 | VOD + Live | WebVTT | 僅VOD |
| 播放 | VOD + Live | 故障轉移 | 僅VOD |
| 播放 | VOD + Live | QoS和播放器通知 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 支援Cookie標頭 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 設定緩衝區控制參數 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 設定自適應比特率控制 | ![](assets/supported15.png) |
| 播放 | VOD + Live | 自定義標籤(EventStream) | 僅VOD（內聯） |
| 播放 | VOD + Live | 延遲綁定音頻 | 僅VOD |
| 播放 | VOD + Live | 302重定向 | 僅VOD |
