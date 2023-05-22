---
description: 使用應用中瀏覽器TVSDK提供的瀏覽器驗證庫檔案建立與瀏覽器相容的播放器。
title: 建立與瀏覽器相容的播放器，而不使用UI-Framework
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 建立與瀏覽器相容的播放器，而不使用UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

使用應用中瀏覽器TVSDK提供的瀏覽器驗證庫檔案建立與瀏覽器相容的播放器。

主題 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 列出了在建立基本視頻播放器時通常包含的瀏覽器TVSDK庫集。 要執行此操作，只需添加 `script` 標籤 `src` 指向庫的屬性。

建立與瀏覽器相容的播放器的過程略有不同。 對於此，您使用 `require` 命令 [!DNL AdobePSDK.module.js] 檔案（由瀏覽器TVSDK提供）。 此檔案將基本播放器庫檔案捆綁在其相應的依賴關係中，並返回 `AdobePSDK` 用於為播放器實現功能的命名空間。

瀏覽器TVSDK在發行包中提供以下瀏覽應用程式和生成檔案示例：

* [!DNL] [...]/samples/browserify/reference/build/Gruntfile.js
* [!DNL] [...]/samples/browserify/reference/build/package.json
* [!DNL] [...]/samples/browserify/reference/examples/sample.html
* [!DNL] [...]/samples/browserify/reference/examples/sample.js

要建立與瀏覽相容的視頻播放器，請執行以下操作：

1. 需要與瀏覽器相容的庫檔案，以返回 `AdobePSDK` 命名空間：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 按中所述建立您的播放器 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md)。

   此任務中的步驟1將替換基本播放器說明中的步驟，在基本播放器說明中，您可以在應用程式檔案中為各個基本播放器庫提供原始碼。
現在，您可以使用瀏覽功能捆綁應用程式檔案。
