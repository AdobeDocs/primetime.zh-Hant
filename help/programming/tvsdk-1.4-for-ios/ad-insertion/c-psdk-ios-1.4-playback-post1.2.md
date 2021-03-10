---
description: 媒體播放的行為會受到搜尋、暫停和廣告的包含所影響。
title: 廣告的預設和自訂播放行為
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# 廣告的預設和自訂播放行為{#default-and-customized-playback-behavior-with-ads}

媒體播放的行為會受到搜尋、暫停和廣告的包含所影響。

若要覆寫預設行為，請使用`PTAdPolicySelector`。

>[!IMPORTANT]
>
>對於VOD和即時／線性串流，時間軸調整無法修訂。 這表示廣告在播放後無法從時間軸移除。 如果使用者返回搜尋，即使一般原則是移除相同的廣告，也會再次播放廣告。

>[!IMPORTANT]
>
>TVSDK不提供在廣告期間停用搜尋的方式。 Adobe建議您將應用程式設定為在廣告期間停用搜尋。

下表說明TVSDK在播放期間如何處理廣告和廣告插播：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 視訊活動 </th> 
   <th colname="col2" class="entry"> 預設TVSDK行為政策 </th> 
   <th colname="col3" class="entry">可通過<span class="codeph"> PTAdPolicySelector</span>進行定制 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期間，會遇到廣告插播。 </td> 
   <td colname="col2"></td> 
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
   <td colname="col3">使用<span class="codeph"> selectAdBreaksToPlay</span>選擇要播放的跳過的中斷，並使用<span class="codeph"> PTAdBreak.isWatched</span>確定已觀看的中斷。 <p> <p>重要： 依預設，TVSDK會在廣告插播中輸入第一個廣告後，立即將廣告插播標示為已觀看的廣告。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會在一或多個廣告插播上向前或向後搜尋，並掉進受觀看的廣告插播。 </td> 
   <td colname="col2"> 跳過廣告插播，並尋找緊接在廣告插播後的位置。 </td> 
   <td colname="col3">使用<span class="codeph"> selectPolicyForSeekIntoAd</span>為廣告插播（監視狀態設為true）和特定廣告指定不同的廣告原則，以便搜尋結束。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會搜尋使用自訂廣告標籤插入的廣告。 </td> 
   <td colname="col2"> 跳至使用者選取的搜尋位置。 </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>

