---
description: MediaResource類別代表MediaPlayer例項要載入的內容。
title: 建立媒體資源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

MediaResource類別代表MediaPlayer例項要載入的內容。

1. 建立 `MediaResource` 將媒體的相關資訊傳送至 `MediaResource` 建構函式。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 建構函式引數 </th> 
    <th colname="col2" class="entry"> 說明 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>字串，代表媒體的資訊清單/播放清單的URL。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>下列成員之一 <span class="codeph"> MediaResource.Type </span> 對應到指定檔案型別的列舉： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO基本媒體檔案格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 虛線 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>中繼資料 </p> </td> 
    <td colname="col2"> <p>的例項 <span class="codeph"> 中繼資料 </span> 類別，其中可能包含要載入之內容的自訂資訊。 內容範例為要置於主要內容內的替代或廣告內容。 如果使用廣告，請設定 <span class="codeph"> Auditudesettings </span> 使用此建構函式之前。 如需詳細資訊，請參閱 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Flash提示：如有需要，您可以使用 <span class="codeph"> forceFlash </span> 引數。 此功能相當實用，因為瀏覽器TVSDK目前並不支援所有功能（例如即時廣告工作流程）。 Flash遞補用於播放視訊內容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >瀏覽器TVSDK僅支援特定內容型別的播放。 如果您嘗試載入任何其他型別的內容，瀏覽器TVSDK會傳送錯誤事件。

   下列程式碼會建立 `MediaResource` 例項：

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
   >在此之後的任何時間，您都可以使用 `MediaResource` 存取子(getter) ，用於檢查資源的型別、URL和中繼資料。

1. 載入MediaPlayer例項。 如需詳細資訊，請參閱 [在MediaPlayer中載入媒體資源](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
