---
description: 可以使用瀏覽器TVSDK提供的JS檔案建立與瀏覽器相容的播放器。
title: 與瀏覽相容的播放器
exl-id: 3e9751d8-7a7e-465b-8d46-d07e4ccb1f5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# 概述 {#browserify-compatible-player-overview}

可以使用瀏覽器TVSDK提供的JS檔案建立與瀏覽器相容的播放器。

瀏覽器TVSDK提供兩個與瀏覽相容的JS檔案。 一種是與AdobePSDK模組一起使用；這是用於開發沒有UI-Framework的應用。 二是與UI-Framework模組一起使用；它返回您使用UI-Framework編寫應用時使用的PTP命名空間。

要開始瀏覽，請運行以下安裝命令以建立 [!DNL final.js] 檔案（瀏覽包檔案） [!DNL example] 目錄 [!DNL samples/browerify/reference] 和 [!DNL samples/browerify/ui-framework]:

1. 導航到 [!DNL samples/browserify/reference/build]。
1. 運行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 導航到 [!DNL samples/browserify/ui-framework/build]。
1. 運行與步驟2中相同的命令。

完成此設定後，您可以根據TVSDK提供的示例繼續建立與瀏覽相容的TVSDK應用。
