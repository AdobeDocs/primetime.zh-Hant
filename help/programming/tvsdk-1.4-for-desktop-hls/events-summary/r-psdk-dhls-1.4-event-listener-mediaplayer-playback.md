---
description: 您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器的變更狀態。
title: 播放事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 播放事件 {#playback-events}

您的應用程式可監聽TVSDK傳送的事件，以監控播放器中的活動和播放器的變更狀態。

TVSDK會在媒體播放作業發生時（例如視訊開始播放），傳送播放事件。 若要收到有關所有播放相關事件的通知，請使用 `MediaPlayer` 物件。

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 事件 </th> 
   <th colname="2" class="entry"> 含義 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> 已選取的速率</a> </td> 
   <td colname="2"> 使用者或TVSDK已選取新的播放速率，例如快進、倒帶或以正常速度繼續播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> 畫面上會顯示新的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> 媒體目前的播放點位置已變更。 目前時間變更時定期傳送，每250毫秒或更長時間傳送一次。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>媒體播放器</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGE</a> </td> 
   <td colname="2"> 媒體播放器的狀態已變更。 您的應用程式應處理此事件回呼中的錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> 設定檔已變更</a> </td> 
   <td colname="2">媒體播放器目前的設定檔已變更。 使用 <span class="codeph"> ProfileEvent.profile</span> 屬性來取得正在播放的新設定檔。 使用 <span class="codeph"> 時間</span> 屬性以取得此事件發生的時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> 「 」已建立。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> 專案已更新</a> </td> 
   <td colname="2">在下列任一情況下，媒體播放器都已成功更新媒體： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">當即時資產發生資訊清單重新整理時。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">當VOD或即時資產具有隱藏式字幕且首次探索隱藏式字幕追蹤的活動時。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>註解與音訊</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> 標題已更新</a> </td> 
   <td colname="2">在媒體串流中偵測到新的隱藏式字幕曲目，而且 <span class="codeph"> closedCaptionsTracks</span> 已更新集合。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>資訊清單和時間表</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">時間軸事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> 時間軸已更新</a> </td> 
   <td colname="2">媒體播放器已新增或移除廣告，因此具有更新的時間軸。 <p>已針對即時資產重新整理資訊清單，並從時間軸移除舊的廣告插播，或是探索到新的廣告機會（提示點）。 媒體播放器會嘗試解決此問題，並將任何新廣告置於時間軸上。 </p> <p> 使用此事件來檢查時間軸是否有任何更新（播放期間VOD不會變更）。 您接著可以使用擷取時間軸 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
