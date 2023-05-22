---
description: 使用幫助程式類AuditudeSettings（擴展MetadataNode類）來設定Adobe Primetime和確定元資料。
title: 設定和插入元資料
exl-id: f7d1eb7d-e0be-4f0f-9dec-9336641a8f87
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 設定和插入元資料 {#set-up-ad-insertion-metadata}

使用幫助程式類 `AuditudeSettings`，它擴展了 `MetadataNode` 類，用於設定Adobe Primetime和決策元資料。

>[!TIP]
>
>Adobe Primetime的廣告決定之前被稱為奧迪。

廣告元資料位於 `MediaResource.Metadata` 屬性。 開始播放新視頻時，應用程式負責設定正確的廣告元資料。

1. 構建 `AuditudeSettings` 實例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime和決策 `mediaID`。 `zoneID`。 `<ph conkeyref="phrases/primetime-sdk-name"/>`和可選的目標參數。

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
   >媒體ID被TVSDK用作字串，該字串被轉換為md5值，用於 `u` Mighine廣告決策URL請求中的值。 例如：
   >
   >`https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 建立 `MediaResource` 實例。

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. 載入 `MediaResource` 對象 `MediaPlayer.replaceCurrentResource` 的雙曲餘切值。

   的 `MediaPlayer` 開始載入和處理媒體流清單。

1. 當 `MediaPlayer` 轉換為INITIALIZED狀態，獲取媒體流特性，格式為 `MediaPlayerItem` 實例 `MediaPlayer.CurrentItem` 的雙曲餘切值。
1. （可選）查詢 `MediaPlayerItem` 實例，查看流是否處於活動狀態，而不管它是否具有備用音頻軌道或流是否受到保護。

   此資訊可幫助您為回放準備UI。 例如，如果您知道有兩個音頻軌道，則可以包括在這些軌道之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以啟動廣告工作流。

   廣告解析並放在時間表上後， `MediaPlayer` 向 `PREPARED` 狀態。
1. 呼叫 `MediaPlayer.play` 的子菜單。
TVSDK現在在播放媒體時包含廣告。
