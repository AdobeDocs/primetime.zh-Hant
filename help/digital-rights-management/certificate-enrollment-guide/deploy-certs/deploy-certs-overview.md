---
seo-title: 部署憑證概觀
title: 部署憑證概觀
uuid: e6413f9f-69a5-4881-bb13-47a80cf32a48
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 概述{#deploy-certificates-overview}

若要將憑證新增至Adobe Primetime DRM屬性檔案，請使用私密金鑰將PKCS#7檔案轉換為PFX檔案，並產生PEM檔案或DER檔案。

* 當需要憑證（憑證和私密金鑰）時，Primetime DRM命令列工具和Adobe HTTP Dynamic Streaming Packager需要PFX檔案。 SDK、參考實作和Primetime DRM Server for Protected Streaming可以接受PFX檔案，也可以使用儲存在HSM上的憑證。
* 當只需要憑證時，大部分的Primetime DRM元件都可在HSM上使用PEM檔案、DER檔案或憑證。 Adobe HTTP Dynamic Streaming Packager僅接受DER檔案做為憑證。