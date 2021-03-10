---
description: 使用輔助類AuditudeSettings（可擴充MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。
title: 設定廣告插入中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 設定廣告插入中繼資料{#set-up-ad-insertion-metadata}

使用延伸`MetadataNode`類別的輔助類別`AuditudeSettings`來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime廣告決策之前稱為Auditude。

廣告中繼資料位於`MediaResource.Metadata`屬性中。 當開始播放新視訊時，您的應用程式負責設定正確的廣告中繼資料。

1. 建立`AuditudeSettings`例項。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策`mediaID`、`zoneID`、`<ph conkeyref="phrases/primetime-sdk-name"/>`和選用定位參數。

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
   >媒體ID由TVSDK使用為字串，並轉換為md5值，用於Primetime廣告決策URL請求中的`u`值。 例如：
   >
   >`https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 使用媒體串流URL和先前建立的廣告中繼資料，建立`MediaResource`例項。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 通過`MediaPlayer.replaceCurrentResource`方法載入`MediaResource`對象。

   `MediaPlayer`開始載入並處理媒體串流資訊清單。

1. 當`MediaPlayer`轉換為「已初始化」狀態時，通過`MediaPlayer.CurrentItem`方法以`MediaPlayerItem`實例的形式獲得媒體流特性。
1. （選擇性）查詢`MediaPlayerItem`例項，以查看串流是否為即時，不論串流是否有替代的音軌或串流受到保護。

   這些資訊可協助您準備播放的UI。 例如，如果您知道有兩個音軌，則可加入UI控制項，以在這些音軌之間切換。

1. 呼叫`MediaPlayer.prepareToPlay`以啟動廣告工作流程。

   廣告解析並置於時間軸上後，`MediaPlayer`會轉換為`PREPARED`狀態。
1. 呼叫`MediaPlayer.play`以開始播放。
TVSDK現在會在您的媒體播放時加入廣告。
