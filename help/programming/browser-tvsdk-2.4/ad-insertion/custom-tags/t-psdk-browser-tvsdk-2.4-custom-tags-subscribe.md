---
description: 每次在媒體演示說明(MPD)檔案中遇到這些對象時，瀏覽器TVSDK都會為訂閱的標籤準備TimedMetadata對象。
title: 訂閱自定義廣告標籤
exl-id: d4b9ec3a-9c3f-4adf-984e-b45862e97140
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 訂閱自定義廣告標籤{#subscribe-to-custom-ad-tags}

每次在媒體演示說明(MPD)檔案中遇到這些對象時，瀏覽器TVSDK都會為訂閱的標籤準備TimedMetadata對象。

必須在播放開始前訂閱標籤。
要訂閱標籤，請將包含自定義標籤名稱的向量設定為 `subscribedTags` 屬性。 如果還需要更改預設商機生成器使用的廣告標籤，請將包含自定義廣告標籤名稱的向量設定為 `adTags` 屬性。

要訂閱自定義標籤：

1. 建立新媒體播放器項配置。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 建立空字串向量。

   ```js
   var subscribeTags = [];
   ```

1. 將自定義標籤名稱添加到此向量。

   >[!IMPORTANT]
   >
   >如果要處理HLS流，請記住 `#` 前置詞。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 將更新的向量分配給 `mediaPlayerItemConfig.subscribeTags` 屬性。

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 建立空字串向量。

   ```js
   var adTags= [];
   ```

1. 將自定義廣告標籤名稱添加到此向量。

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 將更新的向量分配給 `mediaPlayerItemConfig.adTags` 屬性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 載入媒體流時使用媒體播放器項配置。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
