---
description: 媒體播放的行為受到查找、暫停、快速前進或倒退（特技播放模式）以及廣告的包含的影響。
title: 使用廣告的預設和自定義播放行為
exl-id: 242a94e7-acc1-4676-b8a7-9652d4fd1e7e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# 使用廣告的預設和自定義播放行為 {#default-and-customized-playback-behavior-with-ads}

媒體播放的行為受到查找、暫停、快速前進或倒退（特技播放模式）以及廣告的包含的影響。

要覆蓋預設行為，請使用 `AdBreakPolicySelector`。

>[!IMPORTANT]
>
>TVSDK不提供在廣告期間禁用搜索的方法。 Adobe建議將應用程式配置為在廣告期間禁用搜索。

下面是即時/線性內容的回放行為：

* 在暫停後繼續播放將導致在暫停時緩衝的內容的播放。

   如果恢復位置仍在回放範圍內，則回放應連續。 否則，TVSDK會跳到新的即時點。 也可以執行查找操作並選取不同的回放點。
* TVSDK在應用程式進入即時播放的位置之後的提示之間解析廣告。

   解析第一個提示後開始播放。 輸入即時播放的預設值是客戶端即時點，但您可以選擇其他位置。 在應用程式在DVR窗口中執行尋道之後，解決初始位置之前的所有提示。

下表介紹了TVSDK在播放過程中如何處理廣告和廣告中斷：

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 視頻活動 </th> 
   <th colname="col2" class="entry"> 預設TVSDK行為策略 </th> 
   <th colname="col3" class="entry">通過 <span class="codeph"> AdBreakPolicySelector </span> </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 在正常播放期間，遇到廣告中斷。 </td> 
   <td colname="col2"> 
    <ul id="ul_10D2638676EA4ADDA718E61BD4FDC1D2"> 
     <li id="li_D5CC30F063934C738971E2E8AF00C137"> 對於即時/線性，即使廣告片段已經被觀看，也會播放廣告片段。 </li> 
     <li id="li_D962C0938DA74186AE99D117E5A74E38">對於VOD，播放廣告片段並將廣告片段標籤為觀看。 </li> 
    </ul> </td> 
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
   <td colname="col3">選擇使用 <span class="codeph"> 選擇AdBreaksToPlay</span> 並確定已使用 <span class="codeph"> AdBreak.isStated</span>。 <p>重要提示：預設情況下，TVSDK在進入廣告分段中的第一個廣告後立即將廣告分段標籤為監視。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式在一個或多個廣告中查找向前或向後，並跳入已監視的廣告中。 </td> 
   <td colname="col2"> 跳過廣告片段，並在廣告片段後立即找到位置。 </td> 
   <td colname="col3">為廣告中斷（監視狀態設定為true）和通過使用 <span class="codeph"> selectPolicyForSeekIntoAd</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式進入特技播放（DVR模式）。 播放率可為負（倒帶）或大於1（快進）。 </td> 
   <td colname="col2"> 在快進或倒帶期間跳過所有廣告，在特技播放結束後播放跳過的最後一個休息，並在該休息結束回放時跳到用戶選擇的特技播放位置。 </td> 
   <td colname="col3">使用 <span class="codeph"> 選擇AdBreaksToPlay</span>。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 您的應用程式將查找使用自定義廣告標籤插入的廣告。 </td> 
   <td colname="col2"> 跳至用戶選擇的查找位置。 </td> 
   <td colname="col3">有關詳細資訊，請參見 <a href="../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-seek-scrub-bar-display.md">顯示具有當前回放位置的查找擦除欄</a>。 </td> 
  </tr> 
 </tbody> 
</table>
