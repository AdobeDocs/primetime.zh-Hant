---
description: 您可以自訂廣告插入中繼資料。
title: 自訂廣告插入中繼資料
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 自訂廣告插入中繼資料{#customize-ad-insertion-metadata}

您可以自訂廣告插入中繼資料。

1. 為未解決的機會設定廣告元資料的超時。

   此逾時的預設值為20秒。
1. 要將值更改為10秒，請輸入以下內容：

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   `timeout`屬性定義在`AdvertisingMetadata`類別中，且可針對從`AdvertisingMetadata`類別衍生的任何自訂廣告設定設定設定此逾時。 例如，如果使用者為FreeWheel解析器定義自訂設定，則可使用此設定來設定預設逾時。

1. 使用步驟2中的廣告設定建立`MediaPlayerItemConfig`。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. 在`MediaPlayer`上呼叫`replaceCurrentResource`時，請使用此配置。

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

