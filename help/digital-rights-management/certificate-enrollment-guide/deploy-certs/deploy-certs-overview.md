---
title: 部署證書概述
description: 部署證書概述
copied-description: true
exl-id: 45a4bc7e-f987-4b9a-885d-d989d09566c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 概述 {#deploy-certificates-overview}

要向Adobe PrimetimeDRM屬性檔案添加證書，請使用私鑰將PKCS#7檔案轉換為PFX檔案，並生成PEM檔案或DER檔案。

* 當需要憑據（證書和私鑰）時，黃金時段DRM命令行工具和AdobeHTTP Dynamic Streaming包程式需要PFX檔案。 SDK、參考實現和黃金時段DRM Server用於受保護的流管理可以接受PFX檔案，也可以使用儲存在HSM上的憑據。
* 當僅需要證書時，大多數黃金時段DRM元件可以在HSM上使用PEM檔案、DER檔案或證書。 AdobeHTTP Dynamic Streaming打包器只接受DER檔案作為證書。
