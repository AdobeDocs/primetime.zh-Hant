---
description: MediaResource類別代表MediaPlayer例項要載入的內容。
title: 建立媒體資源
exl-id: 754515e9-567d-4f9f-911d-e9dad22f71a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

對於每個新視訊內容，使用視訊內容的資訊初始化MediaResource例項並載入媒體資源。

MediaResource類別代表MediaPlayer例項要載入的內容。

1. 建立 `MediaResource` 將媒體的相關資訊傳送至 `MediaResource` 建構函式。

   此 `MediaResource` 建構函式需要下列引數：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> 建構函式引數 </th>
      <th colname="col2" class="entry"> 說明 </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url </span> </td>
      <td colname="col2"> 代表媒體資訊清單/播放清單URL的字串。 </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type </span> </td>
      <td colname="col2"> 下列成員之一 <span class="codeph"> MediaResource.Type </span> 列舉，對應到指示的檔案型別：
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO基本媒體檔案格式(MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 虛線 </span> - MPEG虛線媒體簡報說明(MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 中繼資料 </span> </td>
      <td colname="col2"> 的例項 <span class="codeph"> 中繼資料 </span> 類別（類似字典的結構），可能包含即將載入之內容的額外資訊，例如要置於主要內容內的替代或廣告內容。 如果使用廣告，請設定 <span class="codeph"> Auditudesettings </span> 使用此建構函式之前。 </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定內容型別的播放。 如果您嘗試載入任何其他型別的內容，TVSDK會傳送錯誤事件。
   >
   >針對MP4隨選視訊(VOD)內容，TVSDK不支援特技播放、調適型位元速率(ABR)串流、廣告插入、隱藏式字幕或DRM。

   下列程式碼會建立 `MediaResource` 例項：

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   在此步驟後的任何時間，您都可以使用 `MediaResource` 存取子(getter)，檢查資源的型別、URL和中繼資料。

1. 使用下列其中一個選項載入媒體資源：

   * MediaPlayer例項。
   * `MediaPlayerItemLoader` 如需詳細資訊，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >請勿在背景執行緒上載入媒體資源。 大部分的TVSDK操作都需要在主要執行緒上執行，而在背景執行緒上執行這些操作可能會導致操作擲回錯誤並退出。
