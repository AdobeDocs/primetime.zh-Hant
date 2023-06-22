---
title: 部署憑證概述
description: 部署憑證概述
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 概觀 {#deploy-certificates-overview}

若要將憑證加入Adobe Primetime DRM屬性檔案，請使用私密金鑰將PKCS#7檔案轉換為PFX檔案，並產生PEM檔案或DER檔案。

* 當需要認證（憑證和私密金鑰）時，Primetime DRM命令列工具和AdobeHTTP Dynamic Streaming封裝程式需要PFX檔案。 SDK、Reference Implementation和Primetime DRM Server for Protected Streaming可以接受PFX檔案，也可以使用儲存在HSM上的認證。
* 當只需要憑證時，大多數Primetime DRM元件都可以使用PEM檔案、DER檔案或HSM上的憑證。 AdobeHTTP Dynamic Streaming封裝程式只接受憑證的DER檔案。
