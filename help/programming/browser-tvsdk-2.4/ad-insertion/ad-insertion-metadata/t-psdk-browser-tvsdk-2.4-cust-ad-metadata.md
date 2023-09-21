---
description: 您可以自訂廣告插入中繼資料。
title: 自訂廣告插入中繼資料
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 自訂廣告插入中繼資料{#customize-ad-insertion-metadata}

您可以自訂廣告插入中繼資料。

1. 針對未解決的機會，在廣告中繼資料上設定逾時。

   此逾時的預設值為20秒。
1. 若要將值變更為10秒，請輸入下列內容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   此 `timeout` 屬性定義於 `AdvertisingMetadata` 類別，而且此逾時是針對任何衍生自的自訂廣告設定所設定。 `AdvertisingMetadata` 類別。 例如，如果使用者為FreeWheel解析器定義自訂設定，他們可以使用這個設定來設定預設逾時。

1. 建立 `MediaPlayerItemConfig` ，並使用步驟2中的廣告設定。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 呼叫時使用此設定 `replaceCurrentResource` 於 `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
