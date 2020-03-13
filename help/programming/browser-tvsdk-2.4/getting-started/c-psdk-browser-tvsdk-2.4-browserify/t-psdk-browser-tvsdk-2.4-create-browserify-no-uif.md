---
description: 使用您應用程式中瀏覽器TVSDK提供的「瀏覽器化」程式庫檔案，建立與瀏覽器化相容的播放器。
seo-description: 使用您應用程式中瀏覽器TVSDK提供的「瀏覽器化」程式庫檔案，建立與瀏覽器化相容的播放器。
seo-title: 建立不含UI-Framework的瀏覽器相容播放器
title: 建立不含UI-Framework的瀏覽器相容播放器
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 建立不含UI-Framework的瀏覽器相容播放器{#create-a-browserify-compatible-player-without-the-ui-framework}

使用您應用程式中瀏覽器TVSDK提供的「瀏覽器化」程式庫檔案，建立與瀏覽器化相容的播放器。

本主題 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 列出您建立基本視訊播放器時通常包含的瀏覽器TVSDK程式庫集。 若要這麼做，您只需新增 `script` 指向程式 `src` 庫的屬性標籤。

建立與瀏覽器相容的播放器的程式稍有不同。 因此，您會使用命 `require` 令在應用程 [!DNL AdobePSDK.module.js] 式中加入檔案（由瀏覽器TVSDK提供）。 此檔案會依相依性的適當順序組合基本播放器程式庫檔案，並傳回您用來實作 `AdobePSDK` 播放器功能的命名空間。

瀏覽器TVSDK提供下列範例瀏覽器應用程式，並在發行套件中建立檔案：

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

若要建立與瀏覽器相容的視訊播放器：

1. 需要與瀏覽器相容的程式庫檔案，以傳回命名 `AdobePSDK` 空間：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 如所述，建立您的播放器 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)。

   此工作的步驟1會取代基本播放器指示中的步驟，您在此步驟中會在應用程式檔案中來源化個別的基本播放器程式庫。
您現在可以使用Browserify來整合應用程式檔案。
