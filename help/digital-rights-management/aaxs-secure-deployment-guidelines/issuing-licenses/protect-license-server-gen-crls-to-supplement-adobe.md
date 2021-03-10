---
title: 產生CRL以補充由Adobe發佈的CRL
description: 產生CRL以補充由Adobe發佈的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 生成CRL以補充Adobe{#generate-crls-to-supplement-those-published-by-adobe}發佈的CRL

「Adobe存取」可讓您建立CRL，以補充Adobe所發佈的機器CRL。 Adobe存取SDK會檢查並強制執行AdobeCRL，但是，您可以建立廢止其他電腦憑證的CRL，來禁止其他用戶端電腦。 為此，您必須將CRL傳遞至Adobe存取SDK，然後，在簽發授權時，SDK會檢查AdobeCRL和您自己的CRL。

要瞭解有關生成CRL的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*&#x200B;中的`RevocationListFactory`。
