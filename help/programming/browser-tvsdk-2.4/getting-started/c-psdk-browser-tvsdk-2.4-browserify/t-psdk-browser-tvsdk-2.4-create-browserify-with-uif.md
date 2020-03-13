---
description: 使用您應用程式中的瀏覽器TVSDK提供的瀏覽器化程式庫檔案，使用UI-Framework建立與瀏覽器化相容的播放器。
seo-description: 使用您應用程式中的瀏覽器TVSDK提供的瀏覽器化程式庫檔案，使用UI-Framework建立與瀏覽器化相容的播放器。
seo-title: 使用UI-Framework建立與瀏覽器相容的播放器
title: 使用UI-Framework建立與瀏覽器相容的播放器
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 使用UI-Framework建立與瀏覽器相容的播放器 {#create-a-browserify-compatible-player-using-the-ui-framework}

使用您應用程式中的瀏覽器TVSDK提供的瀏覽器化程式庫檔案，使用UI-Framework建立與瀏覽器化相容的播放器。

TVSDK中包含的範例瀏覽器檔案：

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

若要使用UI-Framework建立與瀏覽器相容的應用程式，您必須在應用程式 `require` 碼中使用兩個瀏覽器化模組（由瀏覽器TVSDK提供）:

1. 需要瀏覽器模組：

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. 按照中所述繼續開發 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md)。
>您現在可以使用Browserify來整合應用程式檔案。
