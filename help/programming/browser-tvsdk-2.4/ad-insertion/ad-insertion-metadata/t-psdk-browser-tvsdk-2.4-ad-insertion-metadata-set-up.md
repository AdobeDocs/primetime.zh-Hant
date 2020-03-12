---
description: 使用輔助類別AuditudeSettings來設定Adobe Primetime廣告決策中繼資料。
seo-description: 使用輔助類別AuditudeSettings來設定Adobe Primetime廣告決策中繼資料。
seo-title: 設定廣告插入中繼資料
title: 設定廣告插入中繼資料
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 設定廣告插入中繼資料{#set-up-ad-insertion-metadata}

使用輔助類別AuditudeSettings來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime廣告決策之前稱為Auditude。

1. 建立實 `AuditudeSettings` 例。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策媒體ID、zoneID、網域和選用的定位參數。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 使用媒 `MediaResource` 體串流URL和先前建立的廣告中繼資料來建立例項。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 通過方 `MediaResource` 法載入對 `MediaPlayer.replaceCurrentResource(resource)` 像。

   開始 `MediaPlayer` 載入和處理媒體串流資訊清單。

1. 當轉換 `MediaPlayer` 為「已初始化」狀態時，通過屬性以實例形式獲得媒 `MediaPlayerItem` 體流特 `MediaPlayer.CurrentItem` 性。
1. （選用）查詢 `MediaPlayerItem` 例項以查看串流是否為即時，不論其是否有替代音軌。

   這些資訊可協助您準備播放的UI。 例如，如果您知道有兩個音軌，則可加入UI控制項，以在這些音軌之間切換。

1. 致電 `MediaPlayer.prepareToPlay` 啟動廣告工作流程。

   廣告解析後並置於時間軸上後，會轉 `  MediaPlayer ` 換為「已準備」狀態。
1. 呼叫 `MediaPlayer.play` 以開始播放。
瀏覽器TVSDK現在會在您的媒體播放時加入廣告。
