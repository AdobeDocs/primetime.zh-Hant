---
description: MediaResource類表示要由MediaPlayer實例載入的內容。
title: 建立媒體資源
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

MediaResource類表示要由MediaPlayer實例載入的內容。

1. 建立 `MediaResource` 通過將有關媒體的資訊 `MediaResource` 建構子。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 建構子參數 </th> 
    <th colname="col2" class="entry"> 說明 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>表示媒體清單/播放清單的URL的字串。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>類型 </p> </td> 
    <td colname="col2"> <p>以下成員之一 <span class="codeph"> MediaResource.Type </span> 與指定的檔案類型對應的枚舉： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO基本媒體檔案格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> 合肥光源 </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 短划線 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元資料 </p> </td> 
    <td colname="col2"> <p>實例 <span class="codeph"> 元資料 </span> 類，可能包含有關要載入的內容的自定義資訊。 內容示例是要放置在主內容內的替代內容或廣告內容。 如果使用廣告，請設定 <span class="codeph"> 音頻設定 </span> 使用此建構子之前。 有關詳細資訊，請參見 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">廣告插入元資料</a>。 </p> <p>提示：如有必要，可以使用 <span class="codeph"> forceFlash </span> 參數。 這很有用，因為當前並非所有功能（如Live Ad工作流）都在瀏覽器TVSDK中受支援。 Flash回退用於播放視頻內容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >瀏覽器TVSDK僅支援特定類型的內容的回放。 如果嘗試載入任何其他類型的內容，瀏覽器TVSDK將派單錯誤事件。

   以下代碼將建立 `MediaResource` 實例：

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
   >在此之後的任何時間， `MediaResource` 訪問器(getter)，用於檢查資源的類型、URL和元資料。

1. 載入MediaPlayer實例。 有關詳細資訊，請參見 [在MediaPlayer中載入媒體資源](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md)。
