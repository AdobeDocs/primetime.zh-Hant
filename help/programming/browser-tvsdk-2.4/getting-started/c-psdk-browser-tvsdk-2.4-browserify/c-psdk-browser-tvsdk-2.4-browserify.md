---
description: 您可以使用瀏覽器TVSDK提供的JS檔案建立與瀏覽器相容的播放器。
seo-description: 您可以使用瀏覽器TVSDK提供的JS檔案建立與瀏覽器相容的播放器。
seo-title: 瀏覽器相容播放器
title: 瀏覽器相容播放器
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# 概述{#browserify-compatible-player-overview}

您可以使用瀏覽器TVSDK提供的JS檔案建立與瀏覽器相容的播放器。

瀏覽器TVSDK提供兩個與瀏覽器相容的JS檔案。 一種是與AdobePSDK模組搭配使用；這是用於開發沒有UI-Framework的應用程式。 二是與UI-Framework模組一起使用；它會傳回您使用UI-Framework編寫應用程式時使用的PTP命名空間。

要開始使用Browserify，請運行以下設定命令以在[!DNL samples/browerify/reference]和[!DNL samples/browerify/ui-framework]下的[!DNL example]目錄內建立[!DNL final.js]檔案（您的Browserify包檔案）:

1. 導覽至[!DNL samples/browserify/reference/build]。
1. 運行以下命令：

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. 導覽至[!DNL samples/browserify/ui-framework/build]。
1. 執行與步驟2相同的命令。

完成此設定後，您就可以根據TVSDK隨附的範例，繼續建立與瀏覽器相容的TVSDK應用程式。
