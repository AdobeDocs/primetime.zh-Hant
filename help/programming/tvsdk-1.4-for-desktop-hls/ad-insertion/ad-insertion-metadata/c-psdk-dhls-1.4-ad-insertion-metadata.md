---
description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-description: 為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。
seo-title: 廣告插入中繼資料
title: 廣告插入中繼資料
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# 廣告插入中繼資料{#ad-insertion-metadata}

為了讓廣告解析程式運作，廣告提供者（例如Adobe Primetime廣告決策）需要設定值，才能啟用您與提供者的連線。

TVSDK包含Primetime廣告決策程式庫。 您的內容若要包含來自Primetime廣告決策伺服器的廣告，您的應用程式必須提供下列必要的`AuditudeSettings`資訊：

* `mediaID`，這是要播放視訊的唯一識別碼。

   發佈者在將視訊內容和廣告資訊送出至Adobe Primetime廣告決策伺服器時，會指派mediaID。 Primetime廣告決策會使用此ID，從伺服器擷取視訊的相關廣告資訊。

* 由Adobe指派的`zoneID`可識別您的公司或網站。
* 您指派的廣告伺服器的網域。
* 其他定位參數。

   您可以根據您的需求和廣告提供者的需求，加入這些參數。

## 設定廣告插入中繼資料{#set-up-ad-insertion-metadata}

使用輔助類別AuditudeSettings（可延伸MetadataNode類別）來設定Adobe Primetime廣告決策中繼資料。

>[!TIP]
>
>Adobe Primetime廣告決策先前稱為Auditude。

廣告中繼資料位於`MediaResource.metadata`屬性中。 當開始播放新視訊時，您的應用程式負責設定正確的廣告中繼資料。

1. 建立`AuditudeSettings`例項。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime廣告決策媒體ID、zoneID、網域和選用的定位參數。

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >媒體ID由TVSDK使用為字串，並轉換為md5值，用於Primetime廣告決策URL請求中的`u`值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 使用媒體串流URL和先前建立的廣告中繼資料，建立`MediaResource`例項。

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 通過`MediaPlayer.replaceCurrentResource`方法載入`MediaResource`對象。

   `MediaPlayer`開始載入並處理媒體串流資訊清單。

1. （選擇性）查詢`MediaPlayerItem`例項，以查看串流是否為即時，不論其是否具有替代音軌，或是串流是否受到保護。

   這些資訊可協助您準備播放的UI。 例如，如果您知道有兩個音軌，則可加入UI控制項，以在這些音軌之間切換。

1. 呼叫`MediaPlayer.prepareToPlay`以啟動廣告工作流程。

   廣告解析並置於時間軸上後，`MediaPlayer`會轉換為「已準備」狀態。
1. 呼叫`MediaPlayer.play`以開始播放。

TVSDK現在會在您的媒體播放時加入廣告。