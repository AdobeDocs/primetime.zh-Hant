---
description: MediaResource類代表MediaPlayer實例要載入的內容。
title: 建立媒體資源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# 建立媒體資源{#create-a-media-resource}

對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。

MediaResource類代表MediaPlayer實例要載入的內容。

1. 將媒體相關資訊傳遞至`MediaResource`建構函式，以建立`MediaResource`。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 建構函式參數 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>代表媒體資訊清單／播放清單URL的字串。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>與指定的檔案類型對應的以下字串值之一： 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span>  - ISO基本媒體檔案格式(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 中繼資料</span> </td> 
      <td colname="col2"> <p><span class="codeph">中繼資料</span>類別的例項，可能包含要載入內容的自訂資訊。 </p> <p>內容的範例是要置於主要內容內的替代或廣告內容。 如果使用廣告，請在使用此建構函式前先設定<span class="codeph"> AuditudeSettings</span>。 如需詳細資訊，請參閱<a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local">Ad Insertion中繼資料</a>。 </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定內容類型的播放。 如果您嘗試載入任何其他類型的內容，TVSDK會派單錯誤事件。
   >
   >對於MP4隨選視訊(VOD)內容，TVSDK不支援特技播放、可調式位元速率(ABR)串流、廣告插入、隱藏字幕或DRM。

   以下代碼建立`MediaResource`實例：

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >此時，您可以使用`MediaResource`存取器(getters)來檢查資源的類型、URL和中繼資料。

1. 使用下列其中一項來載入媒體資源：

   * 您的MediaPlayer例項。

      如需詳細資訊，請參閱「在Mediaplayer中載入媒體資源」。[](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)
   * A `MediaPlayerItemLoader`如需詳細資訊，請參閱[在Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)中載入媒體資源。

