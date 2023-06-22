---
description: 使用應用程式中瀏覽器TVSDK提供的瀏覽器程式庫檔案，透過UI-Framework建立與瀏覽器相容的播放器。
title: 使用UI-Framework建立與瀏覽器相容的播放器
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 使用UI-Framework建立與瀏覽器相容的播放器 {#create-a-browserify-compatible-player-using-the-ui-framework}

使用應用程式中瀏覽器TVSDK提供的瀏覽器程式庫檔案，透過UI-Framework建立與瀏覽器相容的播放器。

TVSDK中包含的瀏覽器檔案範例：

* [！DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [！DNL [...]/samples/browserify/ui-framework/build/package.json]
* [！DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [！DNL [...]/samples/browserify/ui-framework/examples/sample.js]

若要使用UI-Framework建立與瀏覽器相容的應用程式，您必須 `require` 應用程式程式碼中的兩個瀏覽器模組（由瀏覽器TVSDK提供）：

1. 需要瀏覽器模組：

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 依照中的說明繼續開發 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>您現在可以使用Browserify來組合您的應用程式檔案。
