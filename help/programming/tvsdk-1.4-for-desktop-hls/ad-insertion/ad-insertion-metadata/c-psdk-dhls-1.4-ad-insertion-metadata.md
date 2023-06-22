---
description: 為了讓廣告解析程式運作，廣告提供者(例如Adobe Primetime ad decisioning)需要設定值來啟用您與提供者的連線。
title: 廣告插入中繼資料
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 廣告插入中繼資料 {#ad-insertion-metadata}

為了讓廣告解析程式運作，廣告提供者(例如Adobe Primetime ad decisioning)需要設定值來啟用您與提供者的連線。

TVSDK包含Primetime廣告決策程式庫。 若要讓您的內容包含來自Primetime廣告決策伺服器的廣告，您的應用程式必須提供下列必要專案 `AuditudeSettings` 資訊：

* `mediaID`，此為要播放之視訊的唯一識別碼。

   發佈者在將視訊內容和廣告資訊提交至Adobe Primetime廣告決策伺服器時，會指派mediaID。 Primetime廣告決策會使用此ID從伺服器擷取視訊的相關廣告資訊。

* 您的 `zoneID`由Adobe指派，可識別您的公司或網站。
* 您指派的廣告伺服器的網域。
* 其他目標定位引數。

   您可以根據自己的需求和廣告提供者的需求包含這些引數。

## 設定廣告插入中繼資料 {#set-up-ad-insertion-metadata}

使用helper類別AuditudeSettings （這會擴充MetadataNode類別）來設定Adobe Primetime ad decisioning中繼資料。

>[!TIP]
>
>Adobe Primetime ad decisioning先前稱為Auditude。

廣告中繼資料位於 `MediaResource.metadata` 屬性。 開始播放新視訊時，您的應用程式負責設定正確的廣告中繼資料。

1. 建置 `AuditudeSettings` 執行個體。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime ad decisioning mediaID、zoneID、網域，以及選用的鎖定目標引數。

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
   >媒體ID會由TVSDK作為字串使用，然後轉換為一個md5值，並用於 `u` Primetime廣告決策URL請求中的值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 建立 `MediaResource` 使用媒體串流URL和先前建立的廣告中繼資料，執行個體。

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 載入 `MediaResource` 物件穿過 `MediaPlayer.replaceCurrentResource` 方法。

   此 `MediaPlayer` 開始載入及處理媒體資料流資訊清單。

1. （選用）查詢 `MediaPlayerItem` 執行個體以檢視資料流是否為即時，不論其是否有替代音軌，或資料流是否受到保護。

   此資訊可協助您為播放準備UI。 例如，如果您知道有兩個音軌，您可以包含可在這些音軌之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以開始廣告工作流程。

   解析廣告並放置在時間軸上後， `MediaPlayer` 轉換為「已準備」狀態。
1. 呼叫 `MediaPlayer.play` 以開始播放。

TVSDK現在會在您的媒體播放時包含廣告。
