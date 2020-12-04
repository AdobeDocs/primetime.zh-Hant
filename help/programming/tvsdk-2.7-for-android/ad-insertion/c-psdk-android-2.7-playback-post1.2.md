---
description: 媒體播放的行為會受到搜尋、暫停、快進或倒轉以及廣告的影響。
seo-description: 媒體播放的行為會受到搜尋、暫停、快進或倒轉以及廣告的影響。
seo-title: 廣告的預設和自訂播放行為
title: 廣告的預設和自訂播放行為
uuid: 272cdfd0-799f-41e5-bf41-1620d48c992a
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---


# 廣告的預設和自訂播放行為{#default-and-customized-playback-behavior-with-ads}

媒體播放的行為會受到搜尋、暫停、快進或倒轉以及廣告的影響。

若要覆寫預設行為，請使用`AdBreakPolicySelector`。

>[!IMPORTANT]
>
>TVSDK不提供在廣告期間停用搜尋的方式。 Adobe建議您將應用程式設定為在廣告期間停用搜尋。

以下是即時／線性內容的播放行為：

* 暫停後繼續播放會導致播放暫停時緩衝的內容。

   如果繼續位置仍在播放範圍中，則播放應持續。 否則，TVSDK會跳至新的即時點。 您也可以執行尋道操作並選擇不同的播放點。
* TVSDK可解析應用程式進入即時播放位置後提示之間的廣告。

   解決第一個提示後，就會開始播放。 輸入即時播放的預設值是用戶端即時點，但您可以選擇不同的位置。 在應用程式在DVR視窗中執行尋道後，解決初始位置之前的所有提示。

下表說明TVSDK在播放期間如何處理廣告和廣告插播：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 視訊活動 </th> 
   <th colname="col2" class="entry"> 預設TVSDK行為政策 </th> 
   <th colname="col3" class="entry">透過<span class="codeph"> AdBreakPolicySelector </span>提供自訂 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期間，會遇到廣告插播。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 對於即時／線性，即使廣告分段已被觀看，仍會播放廣告分段。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">對於VOD，會播放廣告分段，並將廣告分段標示為已觀看。 </li> 
    </ul> </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForAdBreak</span>為廣告插播指定不同的原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會透過廣告插播向前搜尋主要內容。 </td> 
   <td colname="col2"> 當中斷播放完成時，播放上次跳過的未觀看廣告分段，並在所需的搜尋位置繼續播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>選擇要播放的跳過的中斷。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在廣告插播上向後搜尋主要內容。 </td> 
   <td colname="col2"> 跳至所要的搜尋位置，而不會播放廣告插播。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>選擇要播放的跳過的中斷。                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會尋找廣告插播。 </td> 
   <td colname="col2"> 從搜尋結束的廣告開始播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>為廣告插播和特定廣告指定不同的廣告策略，以便搜尋結束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向後搜尋廣告插播。 </td> 
   <td colname="col2"> 從搜尋結束的廣告開始播放。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>為廣告插播和搜尋結束的特定廣告指定不同的廣告原則。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在主要內容中搜尋前向或後向的已觀看廣告片段。 </td> 
   <td colname="col2"> 如果已監視最後一個跳過的廣告分段，請跳至使用者選取的搜尋位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>選擇要播放的跳過分段，並使用<span class="codeph"> AdBreak.isWatched</span>確定已觀看的分段。 <p>重要： 依預設，TVSDK會在廣告插播中輸入第一個廣告後，立即將廣告插播標示為已觀看的廣告。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在一或多個廣告插播上向前或向後搜尋，並掉進受觀看的廣告插播。 </td> 
   <td colname="col2"> 跳過廣告插播，並尋找緊接在廣告插播後的位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>為廣告插播（監視狀態設為true）和特定廣告指定不同的廣告原則，以便搜尋結束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會進入特技播放（DVR模式）。 播放率可為負（倒轉）或大於1（快進）。 </td> 
   <td colname="col2"> 在快進或倒轉期間跳過所有廣告、在特技播放結束後播放最後跳過的休息，以及在中斷播放結束時跳至使用者選取的特技播放位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>，選取在特技播放結束後要播放的跳過分段。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會搜尋使用自訂廣告標籤插入的廣告。 </td> 
   <td colname="col2"> 跳至使用者選取的搜尋位置。 </td> 
   <td colname="col3">如需詳細資訊，請參閱<a href="../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md" format="dita" scope="local">顯示具有目前播放位置的搜尋拖曳列……</a> </td> 
  </tr> 
 </tbody> 
</table>