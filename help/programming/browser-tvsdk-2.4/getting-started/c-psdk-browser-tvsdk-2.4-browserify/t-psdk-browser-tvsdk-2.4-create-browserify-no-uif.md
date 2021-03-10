---
description: 使用您應用程式中瀏覽器TVSDK提供的「瀏覽器化」程式庫檔案，建立與瀏覽器化相容的播放器。
title: 建立不含UI-Framework的瀏覽器相容播放器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 建立不含UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}的與瀏覽器相容的播放器

使用您應用程式中瀏覽器TVSDK提供的「瀏覽器化」程式庫檔案，建立與瀏覽器化相容的播放器。

主題[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)會列出您建立基本視訊播放器時通常包含的瀏覽器TVSDK程式庫集。 若要這麼做，您只需新增`script`標籤，其中`src`屬性指向程式庫。

建立與瀏覽器相容的播放器的程式稍有不同。 為此，您使用`require`命令，將[!DNL AdobePSDK.module.js]檔案（由瀏覽器TVSDK提供）包含在應用程式中。 此檔案會依相依性的適當順序組合基本播放器程式庫檔案，並傳回您用來實作播放器功能的`AdobePSDK`命名空間。

瀏覽器TVSDK提供下列範例瀏覽器應用程式，並在發行套件中建立檔案：

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

若要建立與瀏覽器相容的視訊播放器：

1. 需要與瀏覽器相容的庫檔案，以返回`AdobePSDK`命名空間：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 按照[](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)中所述建立您的播放器。

   此工作的步驟1會取代基本播放器指示中的步驟，您在此步驟中會在應用程式檔案中來源化個別的基本播放器程式庫。
您現在可以使用Browserify來整合應用程式檔案。
