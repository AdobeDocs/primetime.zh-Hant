---
description: 搜尋、暫停、快進或倒帶（特技播放模式）以及包含廣告都會影響媒體播放行為。
title: 預設和自訂的廣告播放行為
exl-id: 56544683-28a3-4720-bfd8-946cb09880aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# 預設和自訂的廣告播放行為{#default-and-customized-playback-behavior-with-ads}

搜尋、暫停、快進或倒帶（特技播放模式）以及包含廣告都會影響媒體播放行為。

若要覆寫預設行為，請使用 `AdBreakPolicySelector`.

>[!IMPORTANT]
>
>瀏覽器TVSDK不提供在廣告期間停用搜尋的方法。 Adobe建議您將應用程式設定為在廣告期間停用搜尋。

下表說明瀏覽器TVSDK在播放期間如何處理廣告和廣告插播：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 視訊活動 </th> 
   <th colname="col2" class="entry"> 預設瀏覽器TVSDK行為原則 </th> 
   <th colname="col3" class="entry">自訂可透過 <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期間，遇到廣告插播。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 對於即時/線性，即使已觀看廣告插播，也會播放廣告插播。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">對於VOD，會播放廣告插播並將廣告插播標籤為已觀看。 </li> 
    </ul> </td> 
   <td colname="col3">使用為廣告插播指定不同的原則 <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在廣告插播中向前尋找主要內容。 </td> 
   <td colname="col2"> 播放上一個略過的未觀看廣告插播，並在插播播放完成時在所需的搜尋位置繼續播放。 </td> 
   <td colname="col3">使用以下專案選取要播放哪個略過的插播 <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向後搜尋廣告插播，以進入主要內容。 </td> 
   <td colname="col2"> 跳到所需的搜尋位置而不播放廣告插播。 </td> 
   <td colname="col3">使用以下專案選取要播放哪個略過的插播 <span class="codeph"> selectAdBreaksToPlay</span>.                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向前尋找廣告插播。 </td> 
   <td colname="col2"> 從搜尋結束的廣告開始播放。 </td> 
   <td colname="col3">為廣告插播及搜尋結尾的特定廣告指定不同的廣告原則，請使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向後搜尋廣告插播。 </td> 
   <td colname="col2"> 從搜尋結束的廣告開始播放。 </td> 
   <td colname="col3">為廣告插播及搜尋已結束的特定廣告指定不同的廣告原則，使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會透過觀看的廣告插播向前或向後搜尋主要內容。 </td> 
   <td colname="col2"> 如果已觀看最後一個略過的廣告插播，則會跳至使用者選取的搜尋位置。 </td> 
   <td colname="col3">選取要播放的已略過的分隔符號 <span class="codeph"> selectAdBreaksToPlay</span> 並判斷已使用觀看了哪些中斷 <span class="codeph"> iswatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在一或多個廣告插播上向前或向後搜尋，然後掉進觀看的廣告插播。 </td> 
   <td colname="col2"> 略過廣告插播，並尋找緊接在廣告插播之後的位置。 </td> 
   <td colname="col3">為廣告插播（觀看狀態設為true）和搜尋結束的特定廣告指定不同的廣告原則，使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向前搜尋使用自訂廣告標籤插入的廣告。 </td> 
   <td colname="col2"> 略過至使用者選取的搜尋位置。 </td> 
   <td colname="col3">如需詳細資訊，請參閱 <a href="../../browser-tvsdk-2.4/content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-seek-scrub-bar-display.md" format="dita" scope="local"> 使用搜尋列時處理搜尋</a> </td> 
  </tr> 
 </tbody> 
</table>

## 設定自訂廣告行為 {#section_custom_ad_behaviors}

您可以在廣告內容工廠中設定您偏好的行為，位置為 `retrieveAdPolicySelectorCallbackFunc` 方法。 您可以使用 `selectPolicyForAdBreak`， `selectWatchedPolicyForAdBreak`， `selectPolicyForSeekIntoAd`、和 `selectAdBreaksToPlay` 內容處理站中選取原則的方法。
