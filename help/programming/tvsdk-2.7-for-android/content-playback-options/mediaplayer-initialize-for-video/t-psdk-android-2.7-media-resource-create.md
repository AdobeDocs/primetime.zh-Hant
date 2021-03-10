---
description: MediaResource類代表MediaPlayer實例要載入的內容。
title: 建立媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 建立媒體資源{#create-a-media-resource}

對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。

MediaResource類代表MediaPlayer實例要載入的內容。

1. 將媒體相關資訊傳遞至`MediaResource`建構函式，以建立`MediaResource`。

   `MediaResource`建構函式需要下列參數：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> 建構函式參數 </th>
      <th colname="col2" class="entry"> 說明 </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url  </span> </td>
      <td colname="col2"> 代表媒體的資訊清單／播放清單URL的字串。 </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> type  </span> </td>
      <td colname="col2"> <span class="codeph"> MediaResource.Type </span>列舉的下列成員之一，與指定的檔案類型相對應：
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - ISO基本媒體檔案格式(MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - MPEG-DASH媒體簡報說明(MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 中繼資料  </span> </td>
      <td colname="col2"> <span class="codeph">中繼資料</span>類別的例項（類似字典的結構），可能包含有關即將載入內容的其他資訊，例如要置於主內容中的替代或廣告內容。 如果使用廣告，請在使用此建構函式前先設定<span class="codeph"> AuditudeSettings </span>。 </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定內容類型的播放。 如果您嘗試載入任何其他類型的內容，TVSDK會派單錯誤事件。
   >
   >對於MP4隨選視訊(VOD)內容，TVSDK不支援特技播放、可調式位元速率(ABR)串流、廣告插入、隱藏字幕或DRM。

   以下代碼建立`MediaResource`實例：

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   在此步驟之後的任何時間，您都可以使用`MediaResource`存取器(getters)來檢查資源的類型、URL和中繼資料。

1. 使用下列選項之一載入媒體資源：

   * MediaPlayer例項。
   * `MediaPlayerItemLoader` 如需詳細資訊，請參 [閱使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。

   >[!IMPORTANT]
   >
   >不要在後台線程上載入媒體資源。 大部分的TVSDK作業都需要在主執行緒上執行，而在背景執行緒上執行這些作業可能會導致作業擲回錯誤並退出。
