---
description: 您的應用程式可以通過偵聽TVSDK發送的事件來監視播放器中的活動和播放器的更改狀態。
title: 播放事件
exl-id: 9fb77b57-be6c-4dab-b779-d8c606938e46
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# 播放事件 {#playback-events}

您的應用程式可以通過偵聽TVSDK發送的事件來監視播放器中的活動和播放器的更改狀態。

TVSDK在媒體播放操作（例如開始播放的視頻）發生時調度播放事件。 要獲得有關所有播放相關事件的通知，請向 `MediaPlayer` 對象。

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
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> 選定速率</a> </td> 
   <td colname="2"> 用戶或TVSDK選擇了新的播放速率，例如以正常速度快進、倒帶或繼續播放。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> 播放速率</a> </td> 
   <td colname="2"> 螢幕上可看到新的播放速率。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> 更改時間</a> </td> 
   <td colname="2"> 媒體的當前播放頭位置已更改。 當當前時間更改時，每隔250毫秒或更長時間定期派送一次。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>媒體播放器</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> 狀態_更改</a> </td> 
   <td colname="2"> 媒體播放器的狀態已更改。 您的應用程式應處理此事件回調中的錯誤。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">配置檔案事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> 配置檔案(_C)</a> </td> 
   <td colname="2">媒體播放器的當前配置檔案已更改。 使用 <span class="codeph"> ProfileEvent.profile</span> 獲取正在播放的新配置檔案。 使用 <span class="codeph"> 時間</span> 屬性，以獲取發生此事件的時間。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>媒體播放器項</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> 建立項</a> </td> 
   <td colname="2">A <span class="codeph"> 媒體播放器項</span> 已建立。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> 更新的項</a> </td> 
   <td colname="2">媒體播放器已成功更新以下任一情況下的媒體： 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">當即時資產的清單刷新時。 </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">當VOD或即時資產具有關閉字幕並且首次發現用於關閉字幕軌道的活動時。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>字幕和音頻</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> MediaPlayerItem事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">在媒體流和 <span class="codeph"> closedCaptionsTracks</span> 集合已更新。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>清單和時間軸</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">時間軸事件。<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> 時間軸_已更新</a> </td> 
   <td colname="2">媒體播放器已添加或刪除廣告，因此它具有更新的時間線。 <p>為即時資產刷新的清單和舊廣告中斷已從時間線中刪除，或者發現了新廣告機會（提示點）。 媒體播放器嘗試解析並將任何新廣告放在時間軸上。 </p> <p> 使用此事件檢查時間線是否有任何更新（播放期間VOD不會更改）。 然後，可使用 <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>
