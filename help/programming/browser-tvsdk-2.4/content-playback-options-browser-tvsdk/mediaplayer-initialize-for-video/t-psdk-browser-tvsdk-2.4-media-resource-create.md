---
description: MediaResource類代表MediaPlayer實例要載入的內容。
seo-description: MediaResource類代表MediaPlayer實例要載入的內容。
seo-title: 建立媒體資源
title: 建立媒體資源
uuid: c25c037e-e9a0-430c-a150-b75a9ac051b1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 建立媒體資源{#create-a-media-resource}

MediaResource類代表MediaPlayer實例要載入的內容。

1. 將媒體相關資訊傳遞至`MediaResource`建構函式，以建立`MediaResource`。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 建構函式參數 </th> 
    <th colname="col2" class="entry"> 說明 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>代表媒體資訊清單／播放清單URL的字串。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p><span class="codeph"> MediaResource.Type </span>枚舉的下列成員之一，該枚舉與指定的檔案類型相對應： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4  </span> - ISO基本媒體檔案格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 破折 </span> 線- MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>中繼資料 </p> </td> 
    <td colname="col2"> <p><span class="codeph">中繼資料</span>類別的例項，可能包含要載入內容的自訂資訊。 內容的範例是要置於主要內容內的替代或廣告內容。 如果使用廣告，請在使用此建構函式前先設定<span class="codeph"> AuditudeSettings </span>。 如需詳細資訊，請參閱<a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>。 </p> <p>提示： 如有必要，您可使用<span class="codeph"> forceFlash </span>參數來強制Flash備援，以建立媒體資源。 這可能很有用，因為目前並非瀏覽器TVSDK支援所有功能（例如即時廣告工作流程）。 Flash備援功能可用來播放視訊內容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >瀏覽器TVSDK僅支援播放特定類型的內容。 如果您嘗試載入任何其他類型的內容，瀏覽器TVSDK會派單錯誤事件。

   以下代碼建立`MediaResource`實例：

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >在此之後，您隨時都可以使用`MediaResource`存取器(getters)來檢查資源的類型、URL和中繼資料。

1. 載入您的MediaPlayer例項。 如需詳細資訊，請參閱「在MediaPlayer中載入媒體資源」。[](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md)
