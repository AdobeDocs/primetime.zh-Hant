---
description: 您可以自訂廣告插入中繼資料。
seo-description: 您可以自訂廣告插入中繼資料。
seo-title: 自訂廣告插入中繼資料
title: 自訂廣告插入中繼資料
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 自訂廣告插入中繼資料{#customize-ad-insertion-metadata}

您可以自訂廣告插入中繼資料。

1. 為未解決的機會設定廣告元資料的超時。

   此逾時的預設值為20秒。
1. 要將值更改為10秒，請輸入以下內容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   屬 `timeout` 性是在類別中定 `AdvertisingMetadata` 義的，而且可針對任何從類別衍生而來的自訂廣告設定設定此逾 `AdvertisingMetadata` 時。 例如，如果使用者為FreeWheel解析器定義自訂設定，則可使用此設定來設定預設逾時。

1. 使用 `MediaPlayerItemConfig` 步驟2中的廣告設定進行創作。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 在呼叫時使用此 `replaceCurrentResource` 配置 `MediaPlayer`。

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

