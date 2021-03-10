---
description: 使用輔助類別AuditudeSettings來設定Adobe Primetime廣告決策中繼資料。
title: 設定廣告插入中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 設定廣告插入中繼資料{#set-up-ad-insertion-metadata}

使用輔助類別AuditudeSettings來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime廣告決策之前稱為Auditude。

1. 建立`AuditudeSettings`例項。

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策媒體ID、zoneID、網域和選用的定位參數。

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. 使用媒體串流URL和先前建立的廣告中繼資料，建立`MediaResource`例項。

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. 通過`MediaPlayer.replaceCurrentResource(resource)`方法載入`MediaResource`對象。

   `MediaPlayer`開始載入並處理媒體串流資訊清單。

1. 當`MediaPlayer`轉換為「已初始化」狀態時，通過`MediaPlayer.CurrentItem`屬性以`MediaPlayerItem`實例的形式獲得媒體流特性。
1. （選用）查詢`MediaPlayerItem`例項，以查看串流是否為即時，無論其是否具有替代音軌。

   這些資訊可協助您準備播放的UI。 例如，如果您知道有兩個音軌，則可加入UI控制項，以在這些音軌之間切換。

1. 呼叫`MediaPlayer.prepareToPlay`以啟動廣告工作流程。

   廣告解析並置於時間軸上後，`  MediaPlayer `會轉換為「已準備」狀態。
1. 呼叫`MediaPlayer.play`以開始播放。
瀏覽器TVSDK現在會在您的媒體播放時加入廣告。
