---
description: 瀏覽器TVSDK會在每次在媒體簡報描述(MPD)檔案中遇到這些物件時，為訂閱的標籤準備TimedMetadata物件。
title: 訂閱自訂廣告標籤
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 訂閱自訂廣告標籤{#subscribe-to-custom-ad-tags}

瀏覽器TVSDK會在每次在媒體簡報描述(MPD)檔案中遇到這些物件時，為訂閱的標籤準備TimedMetadata物件。

您必須先訂閱標籤，才能開始播放。
若要訂閱標籤，請將包含自訂標籤名稱的向量設定為`subscribedTags`屬性。 如果您還需要更改預設業務機會生成器使用的廣告標籤，請將包含自定義廣告標籤名稱的向量設定為`adTags`屬性。

若要訂閱自訂標籤：

1. 建立新的媒體播放器項目設定。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 建立空字串向量。

   ```js
   var subscribeTags = [];
   ```

1. 新增自訂標籤名稱至此向量。

   >[!IMPORTANT]
   >
   >如果您正在處理HLS流，請記得包含`#`前置詞。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 將更新的向量指派至`mediaPlayerItemConfig.subscribeTags`屬性。

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 建立空字串向量。

   ```js
   var adTags= [];
   ```

1. 新增自訂廣告標籤名稱至此向量。

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 將更新的向量指派至`mediaPlayerItemConfig.adTags`屬性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 載入媒體串流時，請使用媒體播放器項目設定。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

