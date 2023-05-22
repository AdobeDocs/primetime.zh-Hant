---
description: 要允許廣告解析程式工作，廣告提供程式(如Adobe Primetime廣告決定)需要配置值才能啟用與提供程式的連接。
title: 廣告插入元資料
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 廣告插入元資料 {#ad-insertion-metadata}

要允許廣告解析程式工作，廣告提供程式(如Adobe Primetime廣告決定)需要配置值才能啟用與提供程式的連接。

TVSDK包括黃金時段廣告決策庫。 要使您的內容包括來自黃金時段廣告決策伺服器的廣告，您的應用程式必須提供以下要求 `AuditudeSettings` 資訊：

* `mediaID`，它是要播放的視頻的唯一標識符。

   發佈者在向Adobe Primetime廣告決策伺服器提交視頻內容和廣告資訊時分配媒體ID。 該ID由黃金時段廣告決策用於從伺服器檢索視頻的相關廣告資訊。

* 您 `zoneID`，由Adobe分配，標識您的公司或網站。
* 分配的廣告伺服器的域。
* 其他目標參數。

   您可以根據您的需要和廣告提供商的需要包括這些參數。

## 設定和插入元資料 {#set-up-ad-insertion-metadata}

使用幫助程式類AuditudeSettings（擴展MetadataNode類）來設定Adobe Primetime和確定元資料。

>[!TIP]
>
>Adobe Primetime的廣告決定之前被稱為奧迪。

廣告元資料位於 `MediaResource.metadata` 屬性。 開始播放新視頻時，應用程式負責設定正確的廣告元資料。

1. 構建 `AuditudeSettings` 實例。

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. 設定Adobe Primetime和決策mediaID、zoneID、domain和可選目標參數。

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
   >媒體ID被TVSDK用作字串，該字串被轉換為md5值，用於 `u` Mighine廣告決策URL請求中的值。 例如：
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. 建立 `MediaResource` 實例。

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. 載入 `MediaResource` 對象 `MediaPlayer.replaceCurrentResource` 的雙曲餘切值。

   的 `MediaPlayer` 開始載入和處理媒體流清單。

1. （可選）查詢 `MediaPlayerItem` 實例，查看流是否處於活動狀態，而不管它是否具有備用音頻軌道，或流是否受到保護。

   此資訊可幫助您為回放準備UI。 例如，如果您知道有兩個音頻軌道，則可以包括在這些軌道之間切換的UI控制項。

1. 呼叫 `MediaPlayer.prepareToPlay` 以啟動廣告工作流。

   廣告解析並放在時間表上後， `MediaPlayer` 轉換為PREPARED狀態。
1. 呼叫 `MediaPlayer.play` 的子菜單。

TVSDK現在在播放媒體時包含廣告。
