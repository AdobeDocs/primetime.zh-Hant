---
description: 可以使用Adobe PrimetimeDRM建立CRL，該CRL補充由Adobe發佈的電腦CRL。
title: 生成CRL以補充由Adobe發佈的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 生成CRL以補充由Adobe發佈的CRL{#generating-crls-to-supplement-those-published-by-adobe}

可以使用Adobe PrimetimeDRM建立CRL，該CRL補充由Adobe發佈的電腦CRL。

黃金時段DRM SDK檢查並強制AdobeCRL。 但是，您可以通過建立CRL來禁止其他客戶端電腦，該CRL通過將CRL傳遞到Mogine DRM SDK來撤消其他電腦憑據。 發放許可證時，SDK將檢查AdobeCRL和CRL。

要生成CRL，請參見 [吊銷清單工廠](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
