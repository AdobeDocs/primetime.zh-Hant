---
description: 使用協助程式類別AuditudeSettings來設定Adobe Primetime ad decisioning中繼資料。
title: 設定廣告插入中繼資料
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 設定廣告插入中繼資料{#set-up-ad-insertion-metadata}

使用協助程式類別AuditudeSettings來設定Adobe Primetime ad decisioning中繼資料。

>[!TIP]
>
>Adobe Primetime ad decisioning先前稱為Auditude 。

1. 建置 `AuditudeSettings` 執行個體。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime ad decisioning mediaID、zoneID、網域，以及選用的鎖定目標引數。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 建立 `MediaResource` 使用媒體串流URL和先前建立的廣告中繼資料，執行個體。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 載入 `MediaResource` 物件穿過 `MediaPlayer.replaceCurrentResource(resource)` 方法。

   此 `MediaPlayer` 開始載入及處理媒體資料流資訊清單。

1. 當 `MediaPlayer` 轉換到INITIALIZED狀態，以的格式取得媒體資料流特性 `MediaPlayerItem` 執行個體透過 `MediaPlayer.CurrentItem` 屬性。
1. （選用）查詢 `MediaPlayerItem` 執行個體以檢視串流是否為即時，無論是否有替代音軌。

   此資訊可協助您為播放準備UI。 例如，如果您知道有兩個音軌，您可以包含可在這些音軌之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以開始廣告工作流程。

   解析廣告並放置在時間軸上後， `  MediaPlayer ` 轉換為「已準備」狀態。
1. 呼叫 `MediaPlayer.play` 以開始播放。
瀏覽器TVSDK現在會在您的媒體播放時包含廣告。
