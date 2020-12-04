---
description: 對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。 MediaResource類代表MediaPlayer實例要載入的內容。
seo-description: 對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。 MediaResource類代表MediaPlayer實例要載入的內容。
seo-title: 建立媒體資源
title: 建立媒體資源
uuid: d9fe982a-bedf-445c-b5be-f7918693782a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# 建立媒體資源{#create-a-media-resource}

對於每個新視訊內容，初始化包含視訊內容相關資訊的MediaResource例項並載入媒體資源。 MediaResource類代表MediaPlayer實例要載入的內容。

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
    <td colname="col2"> <p><span class="codeph"> MediaResource.Type </span>枚舉的下列成員之一，該枚舉與指定的檔案類型相對應： 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>中繼資料 </p> </td> 
    <td colname="col2"> <p><span class="codeph">中繼資料</span>類別的例項，可能包含要載入內容的自訂資訊。 </p> <p>內容的範例是要置於主要內容內的替代或廣告內容。 如果使用廣告，請設定<span class="codeph"> AuditudeSettings </span>。 如需詳細資訊，請參閱<a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local">廣告插入中繼資料</a>。 </p> </td> 
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
   >此時，您可以使用`MediaResource`存取器(getters)來檢查資源的類型、URL和中繼資料。

1. 使用以下方法載入媒體資源：

   * 您的MediaPlayer例項。

      如需詳細資訊，請參閱「在MediaPlayer中載入媒體資源」。[](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md)
   * A `MediaPlayerItemLoader`如需詳細資訊，請參閱[使用MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)載入媒體資源。
   >[!IMPORTANT]
   >
   >不要在後台線程上載入媒體資源。 大部分的TVSDK作業都需要在主執行緒上執行，而在背景執行緒上執行這些作業可能會導致作業擲回錯誤並退出。
