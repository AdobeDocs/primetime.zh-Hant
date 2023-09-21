---
description: 您可以使用瀏覽器TVSDK提供的JS檔案來建立與瀏覽器相容的播放器。
title: 瀏覽器相容的播放器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概觀 {#browserify-compatible-player-overview}

您可以使用瀏覽器TVSDK提供的JS檔案來建立與瀏覽器相容的播放器。

瀏覽器TVSDK提供兩個與瀏覽器相容的JS檔案。 一種可與AdobePSDK模組搭配使用，這適用於不使用UI-Framework開發應用程式。 另一個用於UI-Framework模組；它會傳回您用來使用UI-Framework撰寫應用程式的PTP名稱空間。

若要開始使用Browserify，請執行以下安裝命令來建立 [!DNL final.js] 中的檔案（您的Browserify套件組合檔案） [!DNL example] 目錄在 [!DNL samples/browerify/reference] 和 [!DNL samples/browerify/ui-framework]：

1. 瀏覽至 [!DNL samples/browserify/reference/build].
1. 執行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 瀏覽至 [!DNL samples/browserify/ui-framework/build].
1. 執行與步驟2相同的命令。

完成此設定後，您可以繼續根據TVSDK提供的範例，建立與瀏覽器相容的TVSDK應用程式。
