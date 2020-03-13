---
description: 使用輔助類別AuditudeSettings（可延伸MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。
seo-description: 使用輔助類別AuditudeSettings（可延伸MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。
seo-title: 設定廣告插入中繼資料
title: 設定廣告插入中繼資料
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 設定廣告插入中繼資料 {#set-up-ad-insertion-metadata}

使用輔助類別AuditudeSettings（可延伸MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime廣告決策先前稱為Auditude。

廣告中繼資料位於屬 `MediaResource.Metadata` 性中。 當開始播放新視訊時，您的應用程式負責設定正確的廣告中繼資料。

1. 建立實 `AuditudeSettings` 例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策 `mediaID`、 `zoneID``domain`選用定位參數。

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
   >媒體ID由TVSDK使用為字串，並轉換為md5值，用於Primetime廣告決 `u` 策URL請求中的值。 例如：
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

1. 使用媒 `MediaResource` 體串流URL和先前建立的廣告中繼資料來建立例項。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 通過方 `MediaResource` 法載入對 `MediaPlayer.replaceCurrentResource` 像。

   開始 `MediaPlayer` 載入和處理媒體串流資訊清單。

1. 當轉 `MediaPlayer` 換為狀 `INITIALIZED` 態時，透過方法以例項形式取得媒 `MediaPlayerItem` 體串流特 `MediaPlayer.CurrentItem` 性。
1. （選擇性）查詢 `MediaPlayerItem` 例項以查看串流是否為即時，不論其是否具有替代音軌或串流是否受保護。

   這些資訊可協助您準備播放的UI。 例如，如果您知道有兩個音軌，則可加入UI控制項，以在這些音軌之間切換。

1. 致電 `MediaPlayer.prepareToPlay` 啟動廣告工作流程。

   在廣告已解析並置於時間軸上後，會轉 `MediaPlayer` 換為狀 `PREPARED` 態。
1. 呼叫 `MediaPlayer.play` 以開始播放。

TVSDK現在會在您的媒體播放時加入廣告。
