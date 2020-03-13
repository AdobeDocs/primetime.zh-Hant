---
description: 每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。
seo-description: 每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。
seo-title: 訂閱自訂標籤
title: 訂閱自訂標籤
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 訂閱自訂標籤{#subscribe-to-custom-tags}

每次在內容資訊清單中遇到這些物件時，TVSDK會為訂閱的標籤準備TimedMetadata物件。

播放開始前，您必須訂閱標籤。
若要訂閱標籤，請指派包含自訂標籤名稱的向量至屬 `subscribedTags` 性。 如果您還需要變更預設業務機會產生器所使用的廣告標籤，請指派包含自訂廣告標籤名稱的向量至屬 `adTags` 性。

要獲得有關HLS清單中自定義標籤的通知：

1. 將包含自訂標籤的向量指派給，以全域設定自訂廣告標 `subscribeTags` 記名 `MediaPlayerItemConfig`稱。

   >[!IMPORTANT]
   >
   >使用HLS流時必 `#` 須包含前置詞。

   例如：

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. 要全局更改預設業務機會生成器使用的廣告標籤，請為中的屬性分配包含自定義廣告標籤名稱 `adTags` 的向量 `PSDKConfig`。

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. 要使所有全局設定生效，請替換當前資源。

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. 若要設定串流的訂閱標籤名稱，請視需要：
   1. 建立媒體播放器項目設定。

      >[!TIP]
      >
      >最簡單的方式是建立預設的媒體播放器項目設定。

   1. 指定包含自訂標籤的向量 `subscribeTags` 於 `MediaPlayerItemConfig`。

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. 若要變更指定串流中預設業務機會產生器所使用的廣告標籤，請指派包含自訂廣告標籤名稱的向量至 `adTags``mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 若要讓串流的變更生效，在載入媒體串流時，請使用媒體播放器項目設定。

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

