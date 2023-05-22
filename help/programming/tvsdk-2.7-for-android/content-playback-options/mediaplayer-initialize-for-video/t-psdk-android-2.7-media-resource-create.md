---
description: MediaResource類表示要由MediaPlayer實例載入的內容。
title: 建立媒體資源
exl-id: 754515e9-567d-4f9f-911d-e9dad22f71a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 建立媒體資源 {#create-a-media-resource}

對於每個新視頻內容，使用有關視頻內容的資訊初始化MediaResource實例並載入媒體資源。

MediaResource類表示要由MediaPlayer實例載入的內容。

1. 建立 `MediaResource` 通過將有關媒體的資訊 `MediaResource` 建構子。

   的 `MediaResource` 建構子需要以下參數：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> 建構子參數 </th>
      <th colname="col2" class="entry"> 說明 </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url </span> </td>
      <td colname="col2"> 表示媒體清單/播放清單的URL的字串。 </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 類型 </span> </td>
      <td colname="col2"> 以下成員之一 <span class="codeph"> MediaResource.Type </span> 枚舉，與指定的檔案類型對應：
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> 合肥光源 </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> 伊索姆夫 </span> - ISO基本媒體檔案格式(MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 短划線 </span> - MPEG-DASH媒體演示說明(MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 元資料 </span> </td>
      <td colname="col2"> 實例 <span class="codeph"> 元資料 </span> 類（類似字典的結構），它可能包含有關將要載入的內容的附加資訊，如要放置在主內容中的替代內容或廣告內容。 如果使用廣告，請設定 <span class="codeph"> 音頻設定 </span> 使用此建構子之前。 </td>
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
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   在此步驟後的任何時間，您都可以使用 `MediaResource` 訪問器(getter)，用於檢查資源的類型、URL和元資料。

1. 使用以下選項之一載入媒體資源：

   * MediaPlayer實例。
   * `MediaPlayerItemLoader` 有關詳細資訊，請參見 [使用MediaPlayerItemLoader載入媒體資源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。

   >[!IMPORTANT]
   >
   >不要在後台線程上載入媒體資源。 大多數TVSDK操作需要在主線程上運行，而在後台線程上運行這些操作可能會導致操作引發錯誤並退出。
