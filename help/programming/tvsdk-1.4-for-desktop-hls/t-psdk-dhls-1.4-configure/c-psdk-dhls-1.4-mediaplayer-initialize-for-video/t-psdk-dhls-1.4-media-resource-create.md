---
description: MediaResource類表示要由MediaPlayer實例載入的內容。
title: 建立媒體資源
exl-id: 20515e90-cbe4-4945-823a-fe882ed460db
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

對於每個新視頻內容，使用有關視頻內容的資訊初始化MediaResource實例並載入媒體資源。

MediaResource類表示要由MediaPlayer實例載入的內容。

1. 建立 `MediaResource` 通過將有關媒體的資訊 `MediaResource` 建構子。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 建構子參數 </th> 
      <th colname="col2" class="entry"> 說明 </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>表示媒體清單/播放清單的URL的字串。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 類型</span> </td> 
      <td colname="col2"> <p>與指定的檔案類型對應的以下字串值之一： 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO基本媒體檔案格式(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> 合肥光源</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 元資料</span> </td> 
      <td colname="col2"> <p>實例 <span class="codeph"> 元資料</span> 類，可能包含有關要載入的內容的自定義資訊。 </p> <p>內容示例是要放置在主內容內的替代內容或廣告內容。 如果使用廣告，請設定 <span class="codeph"> 音頻設定</span> 使用此建構子之前。 有關詳細資訊，請參見 <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Ad Insertion元資料</a>。 </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK僅支援特定類型的內容的回放。 如果嘗試載入任何其他類型的內容，TVSDK將派單錯誤事件。
   >
   >對於MP4視頻點播(VOD)內容，TVSDK不支援特技播放、自適應比特率(ABR)流、廣告插入、隱藏字幕或DRM。

   以下代碼將建立 `MediaResource` 實例：

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >此時，你可以 `MediaResource` 訪問器(getter)，用於檢查資源的類型、URL和元資料。

1. 使用以下方法之一載入媒體資源：

   * 您的MediaPlayer實例。

      有關詳細資訊，請參見 [在Mediaplayer中載入媒體資源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)。
   * A `MediaPlayerItemLoader` 有關詳細資訊，請參見 [在Mediaplayer中載入媒體資源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)。
