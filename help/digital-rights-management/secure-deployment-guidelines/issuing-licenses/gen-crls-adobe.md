---
description: 您可以使用Adobe PrimetimeDRM來建立CRL，以補充由Adobe發佈的機器CRL。
title: 產生CRL以補充Adobe發佈的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 生成CRL以補充Adobe{#generating-crls-to-supplement-those-published-by-adobe}發佈的CRL

您可以使用Adobe PrimetimeDRM來建立CRL，以補充由Adobe發佈的機器CRL。

Primetime DRM SDK會檢查並強制執行AdobeCRL。 不過，您可以建立CRL，將CRL傳遞至Primetime DRM SDK，以廢止其他電腦認證的CRL，以禁止其他用戶端電腦。 當您核發授權時，SDK會檢查AdobeCRL和您的CRL。

要生成CRL，請參見[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
