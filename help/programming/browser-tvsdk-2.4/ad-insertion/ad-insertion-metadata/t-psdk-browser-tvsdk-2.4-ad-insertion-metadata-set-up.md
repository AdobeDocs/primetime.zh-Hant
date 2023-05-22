---
description: 使用幫助程式類AuditudeSettings設定Adobe Primetime和決策元資料。
title: 設定和插入元資料
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 設定和插入元資料{#set-up-ad-insertion-metadata}

使用幫助程式類AuditudeSettings設定Adobe Primetime和決策元資料。

>[!TIP]
>
>Adobe Primetime的廣告決定之前被稱為奧迪。

1. 構建 `AuditudeSettings` 實例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime和決策mediaID、zoneID、domain和可選目標參數。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 建立 `MediaResource` 實例。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 載入 `MediaResource` 對象 `MediaPlayer.replaceCurrentResource(resource)` 的雙曲餘切值。

   的 `MediaPlayer` 開始載入和處理媒體流清單。

1. 當 `MediaPlayer` 轉換為INITIALIZED狀態，獲取媒體流特性，格式為 `MediaPlayerItem` 實例 `MediaPlayer.CurrentItem` 屬性。
1. （可選）查詢 `MediaPlayerItem` 實例，查看流是否處於活動狀態，而不管它是否具有備用音頻軌道。

   此資訊可幫助您為回放準備UI。 例如，如果您知道有兩個音頻軌道，則可以包括在這些軌道之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以啟動廣告工作流。

   廣告解析並放在時間表上後， `  MediaPlayer ` 轉換為PREPARED狀態。
1. 呼叫 `MediaPlayer.play` 的子菜單。
瀏覽器TVSDK現在在播放媒體時包含廣告。
