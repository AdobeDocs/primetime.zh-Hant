---
title: 部署憑證
description: 部署憑證
copied-description: true
exl-id: 649c4f24-f74e-4529-84a2-65bcd6d7677c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# 部署憑證{#deploy-certificates}

為了避免在「授權伺服器」上以純文字形式提供PFX密碼，「參考實作」和Adobe Primetime DRM Server for Protected Streaming在組態檔中指定時要求加密密碼。 另請參閱 *使用Primetime DRM參考實作* 或 *使用Primetime DRM伺服器* （適用於受保護的串流），以取得執行擾頻公用程式的指示。 其中每個都包含自己的擾碼公用程式，而且加密的密碼在這兩個授權伺服器實作之間不可互換。

若要將憑證和加擾密碼部署至您的授權伺服器，請參閱 *使用Primetime DRM參考實作* 或 *使用Primetime DRM伺服器進行受保護的串流*.
