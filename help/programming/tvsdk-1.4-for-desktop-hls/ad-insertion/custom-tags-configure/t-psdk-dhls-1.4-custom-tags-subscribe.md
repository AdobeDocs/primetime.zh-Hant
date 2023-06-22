---
description: TVSDK會在每次訂閱標籤物件出現在內容資訊清單中時，為這些物件準備TimedMetadata物件。
title: 訂閱自訂標籤
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 訂閱自訂標籤{#subscribe-to-custom-tags}

TVSDK會在每次訂閱標籤物件出現在內容資訊清單中時，為這些物件準備TimedMetadata物件。

在播放開始之前，您必須訂閱標籤。
若要訂閱標籤，請將包含自訂標簽名稱的向量指派給 `subscribedTags` 屬性。 如果您也需要變更預設機會產生器使用的廣告標籤，請將包含自訂廣告標簽名稱的向量指派給 `adTags` 屬性。

若要接收有關HLS資訊清單中自訂標籤的通知：

1. 透過指派包含自訂標籤的向量來全域設定自訂廣告標簽名稱 `subscribeTags` 在 `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >您必須包含 `#` 使用HLS資料流時的首碼。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 若要全域變更預設機會產生器使用的廣告標籤，請將包含自訂廣告標籤名稱的向量指派給 `adTags` 中的屬性 `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 若要讓所有全域設定生效，請取代目前的資源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 若要設定串流的訂閱標籤名稱（如有需要）：
   1. 建立媒體播放器專案設定。

      >[!TIP]
      >
      >最簡單的方式是建立預設媒體播放器專案設定。

   1. 將包含自訂標籤的向量指派給 `subscribeTags` 在 `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 若要變更指定串流中預設機會產生器使用的廣告標籤，請將包含自訂廣告標籤名稱的向量指派給 `adTags` 中的屬性 `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 若要讓串流的變更生效，請在載入媒體串流時，使用媒體播放器專案設定。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
