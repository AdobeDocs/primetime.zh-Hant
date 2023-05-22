---
description: 每次在內容清單中遇到這些對象時，TVSDK都會為訂閱的標籤準備TimedMetadata對象。
title: 訂閱自定義標籤
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 訂閱自定義標籤{#subscribe-to-custom-tags}

每次在內容清單中遇到這些對象時，TVSDK都會為訂閱的標籤準備TimedMetadata對象。

在播放開始之前，您必須訂閱標籤。
要訂閱標籤，請為 `subscribedTags` 屬性。 如果還需要更改預設商機生成器使用的廣告標籤，則將包含自定義廣告標籤名稱的向量分配給 `adTags` 屬性。

要通知有關HLS清單中的自定義標籤：

1. 通過將包含自定義標籤的向量指定給 `subscribeTags` 在 `MediaPlayerItemConfig`。

   >[!IMPORTANT]
   >
   >必須包括 `#` 使用HLS流時的前置詞。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 要全局更改預設商機生成器使用的ad標籤，請將包含自定義ad標籤名稱的向量分配給 `adTags` 物業 `PSDKConfig`。

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局設定生效，請替換當前資源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 要為流設定訂閱的標籤名稱（如果需要）:
   1. 建立媒體播放器項配置。

      >[!TIP]
      >
      >最簡單的方法是建立預設媒體播放器項配置。

   1. 將包含自定義標籤的向量分配給 `subscribeTags` 在 `MediaPlayerItemConfig`。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 要更改指定流中預設機會生成器使用的ad標籤，請將包含自定義ad標籤名稱的向量分配給 `adTags` 物業 `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 要使流的更改生效，在載入媒體流時，請使用媒體播放器項配置。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
