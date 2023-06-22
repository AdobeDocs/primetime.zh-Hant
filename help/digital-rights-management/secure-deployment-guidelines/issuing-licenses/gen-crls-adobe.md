---
description: 您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈的機器CRL。
title: 產生CRL以補充Adobe所發佈的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 產生CRL以補充Adobe所發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM來建立CRL，以補充Adobe所發佈的機器CRL。

Primetime DRM SDK會檢查並強制執行AdobeCRL。 不過，您可以建立CRL，將CRL傳遞至Primetime DRM SDK以撤銷其他電腦認證，藉此禁止使用其他使用者端電腦。 當您核發授權時，SDK會檢查AdobeCRL和您的CRL。

若要產生CRL，請參閱 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
