---
description: 每次在媒體簡報說明(MPD)檔案中遇到訂閱的標籤時，瀏覽器TVSDK都會準備這些物件的TimedMetadata物件。
title: 訂閱自訂廣告標籤
exl-id: d4b9ec3a-9c3f-4adf-984e-b45862e97140
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 訂閱自訂廣告標籤{#subscribe-to-custom-ad-tags}

每次在媒體簡報說明(MPD)檔案中遇到訂閱的標籤時，瀏覽器TVSDK都會準備這些物件的TimedMetadata物件。

您必須在播放開始前訂閱標籤。
若要訂閱標籤，請將包含自訂標簽名稱的向量設定為 `subscribedTags` 屬性。 如果您也需要變更預設機會產生器使用的廣告標籤，請將包含自訂廣告標簽名稱的向量設定為 `adTags` 屬性。

若要訂閱自訂標籤：

1. 建立新的媒體播放器專案設定。

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. 建立空的字串向量。

   ```js
   var subscribeTags = [];
   ```

1. 將自訂標簽名稱新增至此向量。

   >[!IMPORTANT]
   >
   >如果您要處理HLS資料流，請記得加入 `#` 前置詞。

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. 將更新的向量指派給 `mediaPlayerItemConfig.subscribeTags` 屬性。

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. 建立空的字串向量。

   ```js
   var adTags= [];
   ```

1. 將自訂廣告標簽名稱新增至此向量。

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. 將更新的向量指派給 `mediaPlayerItemConfig.adTags` 屬性。

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. 載入媒體資料流時，請使用媒體播放器專案設定。

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
