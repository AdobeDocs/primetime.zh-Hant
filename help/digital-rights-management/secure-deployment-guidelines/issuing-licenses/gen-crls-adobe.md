---
description: 您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈之機器CRL。
seo-description: 您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈之機器CRL。
seo-title: 產生CRL以補充Adobe發佈的CRL
title: 產生CRL以補充Adobe發佈的CRL
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 產生CRL以補充Adobe發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈之機器CRL。

Primetime DRM SDK會檢查並強制執行Adobe CRL。 不過，您可以建立CRL，將CRL傳遞至Primetime DRM SDK，以廢止其他電腦認證的CRL，以禁止其他用戶端電腦。 當您核發授權時，SDK會檢查Adobe CRL和您的CRL。

要生成CRL，請參 [閱RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
