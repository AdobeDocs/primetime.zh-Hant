---
description: 使用協助程式類別AuditudeSettings （擴充MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。
title: 設定廣告插入中繼資料
exl-id: 5afcdd51-a611-4ea9-88e1-5aa15b8a504a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 設定廣告插入中繼資料 {#set-up-ad-insertion-metadata}

使用協助程式類別AuditudeSettings （擴充MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime ad decisioning先前稱為Auditude。

廣告中繼資料位於 `MediaResource.Metadata` 屬性。 開始播放新視訊時，您的應用程式負責設定正確的廣告中繼資料。

1. 建置 `AuditudeSettings` 執行個體。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策 `mediaID`， `zoneID`， `domain`和選用的目標定位引數。

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >媒體ID會由TVSDK作為字串使用，然後轉換為一個md5值，並用於 `u` Primetime廣告決策URL請求中的值。 例如：
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. 建立 `MediaResource` 使用媒體串流URL和先前建立的廣告中繼資料，執行個體。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 載入 `MediaResource` 物件穿過 `MediaPlayer.replaceCurrentResource` 方法。

   此 `MediaPlayer` 開始載入及處理媒體資料流資訊清單。

1. 當 `MediaPlayer` 轉換至 `INITIALIZED` 狀態，以格式取得媒體資料流特性 `MediaPlayerItem` 執行個體透過 `MediaPlayer.CurrentItem` 方法。
1. （選用）查詢 `MediaPlayerItem` 執行個體以檢視資料流是否為即時，不論其是否有替代音軌，或資料流是否受到保護。

   此資訊可協助您為播放準備UI。 例如，如果您知道有兩個音軌，您可以包含可在這些音軌之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以開始廣告工作流程。

   解析廣告並放置在時間軸上後， `MediaPlayer` 轉換至 `PREPARED` 州別。
1. 呼叫 `MediaPlayer.play` 以開始播放。

TVSDK現在會在您的媒體播放時包含廣告。
