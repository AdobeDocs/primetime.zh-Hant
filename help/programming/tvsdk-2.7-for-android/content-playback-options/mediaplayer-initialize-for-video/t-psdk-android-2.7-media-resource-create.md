---
description: MediaResource類代表MediaPlayer實例要載入的內容。
seo-description: MediaResource類代表MediaPlayer實例要載入的內容。
seo-title: 建立媒體資源
title: 建立媒體資源
uuid: f34a11a3-dac2-405e-8632-1d9617cc019d
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# 建立媒體資源 {#create-a-media-resource}

對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。

MediaResource類代表MediaPlayer實例要載入的內容。

1. 將媒體 `MediaResource` 的相關資訊傳遞至建構函式，以建立 `MediaResource` 媒體。

   建構 `MediaResource` 函式需要下列參數：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
      <thead> 
      <tr> 
      <th colname="col1" class="entry"> 建構函式參數 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
      </tr> 
      </thead>
      <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> 代表媒體的資訊清單／播放清單URL的字串。 </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> MediaResource.Type列舉的下列成員之一(與指 <span class="codeph"> 定的檔 </span> 案類型相對應): 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO基本媒體檔案格式(MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH </span> - MPEG-DASH媒體簡報說明(MPD) </li> 
      </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 中繼資料 </span> </td> 
      <td colname="col2"> 中繼資料類別的例項( <span class="codeph"></span> 類似字典的結構)，其中可能包含有關即將載入之內容的其他資訊，例如要置於主要內容內的替代或廣告內容。 如果使用廣告，請在使用 <span class="codeph"> 此建構函 </span> 式前先設定AuditudeSettings(請參閱 <a keyref="ad-insertion-metadata"></a>)。 </td> 
      </tr> 
      </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定內容類型的播放。 如果您嘗試載入任何其他類型的內容，TVSDK會派單錯誤事件。
   >
   >對於MP4隨選視訊(VOD)內容，TVSDK不支援特技播放、可調式位元速率(ABR)串流、廣告插入、隱藏字幕或DRM。

   下列程式碼會建立例 `MediaResource` 項：

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
     MediaResource.Type.HLS, 
     metadata); 
   ```

   在此步驟之後的任何時間，您都可 `MediaResource` 以使用存取器(getter)來檢查資源的類型、URL和中繼資料。

1. 使用下列選項之一載入媒體資源：

   * MediaPlayer例項。
   * `MediaPlayerItemLoader` 如需詳細資訊，請參 [閱使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。
   >[!IMPORTANT]
   >
   >不要在後台線程上載入媒體資源。 大部分的TVSDK作業都需要在主執行緒上執行，而在背景執行緒上執行這些作業可能會導致作業擲回錯誤並退出。
