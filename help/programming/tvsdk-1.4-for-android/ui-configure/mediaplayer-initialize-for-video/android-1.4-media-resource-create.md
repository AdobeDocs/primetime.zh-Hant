---
description: 對於每個新視頻內容，使用有關視頻內容的資訊初始化MediaResource實例並載入媒體資源。 MediaResource類表示要由MediaPlayer實例載入的內容。
title: 建立媒體資源
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

對於每個新視頻內容，使用有關視頻內容的資訊初始化MediaResource實例並載入媒體資源。 MediaResource類表示要由MediaPlayer實例載入的內容。

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
    <td colname="col2"> <p>以下成員之一 <span class="codeph"> MediaResource.Type </span> 與指定的檔案類型對應的枚舉： 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> 合肥光源 </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元資料 </p> </td> 
    <td colname="col2"> <p>實例 <span class="codeph"> 元資料 </span> 類，可能包含有關要載入的內容的自定義資訊。 </p> <p>內容示例是要放置在主內容內的替代內容或廣告內容。 如果使用廣告，請設定 <span class="codeph"> 音頻設定 </span>。 有關詳細資訊，請參見 <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion元資料 </a>。 </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定類型的內容的回放。 如果嘗試載入任何其他類型的內容，TVSDK將派單錯誤事件。
   >
   >對於MP4視頻點播(VOD)內容，TVSDK不支援特技播放、自適應比特率(ABR)流、廣告插入、隱藏字幕或DRM。

   以下代碼將建立 `MediaResource` 實例：

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
   >此時，你可以 `MediaResource` 訪問器(getter)，用於檢查資源的類型、URL和元資料。

1. 使用以下方法載入媒體資源：

   * 您的MediaPlayer實例。

      有關詳細資訊，請參見 [在MediaPlayer中載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md)。
   * A `MediaPlayerItemLoader` 有關詳細資訊，請參見 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)。
   >[!IMPORTANT]
   >
   >不要在後台線程上載入媒體資源。 大多數TVSDK操作需要在主線程上運行，而在後台線程上運行這些操作可能會導致操作引發錯誤並退出。
