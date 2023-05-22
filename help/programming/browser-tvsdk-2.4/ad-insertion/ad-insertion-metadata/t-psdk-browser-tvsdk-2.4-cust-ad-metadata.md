---
description: 您可以自定義和插入元資料。
title: 自定義廣告插入元資料
exl-id: 4881ace6-e97b-448d-8fb4-64e7b69517f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 自定義廣告插入元資料{#customize-ad-insertion-metadata}

您可以自定義和插入元資料。

1. 設定未解決機會的元資料廣告超時。

   此超時的預設值為20秒。
1. 要將值更改為10秒，請輸入以下內容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   的 `timeout` 屬性在 `AdvertisingMetadata` 類，並且可以為從派生的任何自定義廣告設定設定此超時 `AdvertisingMetadata` 類。 例如，如果用戶為FreeWheel解析器定義自定義設定，則他們可以使用此設定設定預設超時。

1. 建立 `MediaPlayerItemConfig` 的FTP伺服器連接設定。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 調用時使用此配置 `replaceCurrentResource` 上 `MediaPlayer`。

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
