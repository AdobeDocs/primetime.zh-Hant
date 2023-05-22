---
description: 媒體播放的行為受尋找、暫停和包括廣告的影響。
title: 使用廣告的預設和自定義播放行為
exl-id: f4b2f317-c580-45a9-ad79-0cfa6c21848b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 使用廣告的預設和自定義播放行為 {#default-and-customized-playback-behavior-with-ads}

媒體播放的行為受尋找、暫停和包括廣告的影響。

要覆蓋預設行為，請使用 `PTAdPolicySelector`。

>[!IMPORTANT]
>
>對於VOD和即時/線性流，時間線調整無法修正。 這意味著播放播發後，無法從時間線中刪除播發。 如果用戶返回搜索，則即使正常策略是刪除該廣告，也會再次播放同一廣告。

>[!IMPORTANT]
>
>TVSDK不提供在廣告期間禁用搜索的方法。 Adobe建議將應用程式配置為在廣告期間禁用搜索。

下表介紹了TVSDK在播放過程中如何處理廣告和廣告中斷：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>視頻活動</b></th> 
   <th colname="col2" class="entry"><b>預設TVSDK行為策略</b></th> 
   <th colname="col3" class="entry"><b>通過PTAdPolicySelector提供自定義</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期間，遇到廣告中斷。 </td> 
   <td colname="col2"></td> 
   <td colname="col3">使用 <span class="codeph"> selectPolicyForAdBreak</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會將廣告段向前搜索到主要內容。 </td> 
   <td colname="col2"> 播放跳過的最後一個未觀看廣告斷點，並在中斷播放完成時在所需的查找位置恢復播放。 </td> 
   <td colname="col3">使用 <span class="codeph"> 選擇AdBreaksToPlay</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會將廣告段向後搜索到主內容。 </td> 
   <td colname="col2"> 跳到所需的尋道位置，而不播放廣告分段。 </td> 
   <td colname="col3">使用 <span class="codeph"> 選擇AdBreaksToPlay</span>。                      </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式將進入廣告時段。 </td> 
   <td colname="col2"> 從搜索結束的廣告開始播放。 </td> 
   <td colname="col3">為廣告中斷和通過使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向後搜索廣告片段。 </td> 
   <td colname="col2"> 從搜索結束的廣告開始播放。 </td> 
   <td colname="col3">為廣告中斷和通過使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式會向前或向後查找監視的廣告內容。 </td> 
   <td colname="col2"> 如果已監視上次跳過的廣告片段，則跳過到用戶選擇的搜索位置。 </td> 
   <td colname="col3">選擇使用 <span class="codeph"> 選擇AdBreaksToPlay</span> 並確定已使用 <span class="codeph"> PTAdBreak.isStaed</span>。 <p> <p>重要提示：預設情況下，TVSDK在進入廣告分段中的第一個廣告後立即將廣告分段標籤為監視。 </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式在一個或多個廣告中查找向前或向後，並跳入已監視的廣告中。 </td> 
   <td colname="col2"> 跳過廣告片段，並在廣告片段後立即找到位置。 </td> 
   <td colname="col3">為廣告中斷（監視狀態設定為true）和通過使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式將查找使用自定義廣告標籤插入的廣告。 </td> 
   <td colname="col2"> 跳至用戶選擇的查找位置。 </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
