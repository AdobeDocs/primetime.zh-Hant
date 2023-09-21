---
title: 產生CRL以補充Adobe所發佈的CRL
description: 產生CRL以補充Adobe所發佈的CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 產生CRL以補充Adobe所發佈的CRL{#generate-crls-to-supplement-those-published-by-adobe}

Adobe存取可讓您建立CRL以補充Adobe所發佈的機器CRL。 Adobe存取SDK會檢查並強制執行AdobeCRL，但您可以建立可撤銷其他電腦認證的CRL，以禁止其他使用者端電腦。 若要這麼做，您必須將CRL傳遞至AdobeAccess SDK，然後在核發授權時，SDK會檢查AdobeCRL和您自己的CRL。

若要進一步瞭解如何產生CRL，請參閱 `RevocationListFactory` 在 *Adobe存取API參考*.
