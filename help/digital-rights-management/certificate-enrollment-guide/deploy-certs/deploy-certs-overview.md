---
title: 部署憑證概觀
description: 部署憑證概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 概述{#deploy-certificates-overview}

要向Adobe PrimetimeDRM屬性檔案添加證書，請使用私鑰將PKCS#7檔案轉換為PFX檔案，並生成PEM檔案或DER檔案。

* 當需要憑證（憑證和私密金鑰）時，Primetime DRM命令列工具和AdobeHTTP Dynamic Streaming封裝程式需要PFX檔案。 SDK、參考實作和Primetime DRM Server for Protected Streaming可以接受PFX檔案，也可以使用儲存在HSM上的憑證。
* 當只需要憑證時，大部分的Primetime DRM元件都可在HSM上使用PEM檔案、DER檔案或憑證。 AdobeHTTP Dynamic Streaming包裝器僅接受證書的DER檔案。