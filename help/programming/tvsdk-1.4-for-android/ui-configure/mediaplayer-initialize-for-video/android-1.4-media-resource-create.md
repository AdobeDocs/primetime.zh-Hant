---
description: 對於每個新視訊內容，使用視訊內容的資訊初始化MediaResource例項並載入媒體資源。 MediaResource類別代表MediaPlayer例項要載入的內容。
title: 建立媒體資源
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

對於每個新視訊內容，使用視訊內容的資訊初始化MediaResource例項並載入媒體資源。 MediaResource類別代表MediaPlayer例項要載入的內容。

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
    <td colname="col2"> <p>代表媒體資訊清單/播放清單URL的字串。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>下列成員之一 <span class="codeph"> MediaResource.Type </span> 對應到指示的檔案型別的列舉： 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>中繼資料 </p> </td> 
    <td colname="col2"> <p>的例項 <span class="codeph"> 中繼資料 </span> 類別，其中可能包含有關要載入之內容的自訂資訊。 </p> <p>內容範例為要放置在主要內容內的替代或廣告內容。 如果使用廣告，請設定 <span class="codeph"> Auditudesettings </span>. 如需詳細資訊，請參閱 <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion中繼資料 </a>. </p> </td> 
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
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >此時，您可以使用 `MediaResource` 存取子(getter)，檢查資源的型別、URL和中繼資料。

1. 使用下列專案載入媒體資源：

   * 您的MediaPlayer例項。

      如需詳細資訊，請參閱 [在MediaPlayer中載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` 如需詳細資訊，請參閱 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >請勿在背景執行緒上載入媒體資源。 大部分的TVSDK操作都需要在主要執行緒上執行，而在背景執行緒上執行它們可能會導致操作擲回錯誤並退出。
