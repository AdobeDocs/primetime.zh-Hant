---
description: 使用應用程式中瀏覽器TVSDK提供的瀏覽器程式庫檔案，建立與瀏覽器相容的播放器。
title: 建立不含UI-Framework且與Browserify相容的播放器
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 建立不含UI-Framework且與Browserify相容的播放器{#create-a-browserify-compatible-player-without-the-ui-framework}

使用應用程式中瀏覽器TVSDK提供的瀏覽器程式庫檔案，建立與瀏覽器相容的播放器。

主題 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) 列出您在建立基本視訊播放器時通常包含的一組瀏覽器TVSDK程式庫。 若要這麼做，您只需新增 `script` 標籤與 `src` 指向資料庫的屬性。

建立與Browserify相容的播放器的程式稍微不同。 為此，請使用 `require` 命令以包含 [!DNL AdobePSDK.module.js] 檔案（由瀏覽器TVSDK提供）。 此檔案會依照基本播放器程式庫檔案的適當相依性順序進行捆綁，並傳回 `AdobePSDK` 您用來為播放器實作功能的名稱空間。

瀏覽器TVSDK提供下列範例瀏覽器應用程式和發行套件中的組建檔案：

* [！DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [！DNL [...]/samples/browserify/reference/build/package.json]
* [！DNL [...]/samples/browserify/reference/examples/sample.html]
* [！DNL [...]/samples/browserify/reference/examples/sample.js]

若要建立相容於Browserify的視訊播放程式：

1. 需要可傳回 `AdobePSDK` 名稱空間：

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. 依照中的說明建立您的播放器 [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   此任務中的步驟1會取代基本播放器指示中的步驟，您可在應用程式檔案中取得個別基本播放器程式庫。
您現在可以使用Browserify來組合您的應用程式檔案。
