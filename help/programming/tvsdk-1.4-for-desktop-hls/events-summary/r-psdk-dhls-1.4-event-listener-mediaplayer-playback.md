---
description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-description: 您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。
seo-title: 播放事件
title: 播放事件
uuid: 6d6491d7-cf25-4130-8388-68b8c028bb71
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# 播放事件{#playback-events}

您的應用程式可監聽TVSDK所傳送的事件，以監控播放器中的活動和播放器的變更狀態。

TVSDK會在媒體播放作業發生時（例如視訊開始播放）分派播放事件。 要獲得有關所有回放相關事件的通知，請向`MediaPlayer`對象註冊以下事件的監聽器。

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 事件 </th> 
   <th colname="2" class="entry"> 意義 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> 使用者或TVSDK已選取新的播放速率，例如以正常速度快進、倒轉或繼續播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 新的播放速率在螢幕上可見。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 媒體的目前播放磁頭位置已變更。 當目前時間變更時，每250毫秒或更長時間定期傳送一次。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> 媒體播放器的狀態已變更。 您的應用程式應處理此事件回呼中的錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">媒體播放器的目前設定檔已變更。 使用<span class="codeph"> ProfileEvent.profile</span>屬性來取得正在播放的新設定檔。 使用<span class="codeph"> time</span>屬性來取得發生此事件的時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">已建立<span class="codeph"> MediaPlayerItem</span>。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">媒體播放器已成功更新其中一種媒體： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">當即時資產發生資訊清單重新整理時。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">當VOD或即時資產具有隱藏字幕時，系統會先針對隱藏字幕軌道發現活動。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>標題和音效</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">在媒體串流中偵測到新的隱藏字幕軌道，並且<span class="codeph"> closedCaptionsTracks</span>系列已更新。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>資訊清單和時間軸</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">時間軸事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> 時間軸已更新</a> </td> 
   <td colname="2">媒體播放器已新增或移除廣告，因此有更新的時間軸。 <p>更新為即時資產的資訊清單已從時間軸移除，或發現新的廣告機會（提示點）。 媒體播放器會嘗試解析任何新廣告，並將其置於時間軸上。 </p> <p> 使用此事件來檢查時間軸是否有任何更新（VOD在播放期間不會變更）。 然後，您可以使用<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>擷取時間軸。 </p> </td> 
  </tr> 
 </tbody> 
</table>

