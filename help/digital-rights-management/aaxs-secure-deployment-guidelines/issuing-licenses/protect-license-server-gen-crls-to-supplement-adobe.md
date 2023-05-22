---
title: 生成CRL以補充由Adobe發佈的CRL
description: 生成CRL以補充由Adobe發佈的CRL
copied-description: true
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 生成CRL以補充由Adobe發佈的CRL{#generate-crls-to-supplement-those-published-by-adobe}

Adobe訪問允許您建立CRL以補充由Adobe發佈的電腦CRL。 Adobe訪問SDK會檢查並強制AdobeCRL，但是，您可以通過建立撤銷其他電腦憑據的CRL來禁止附加客戶機。 為此，必須將CRL傳遞給Adobe訪問SDK，然後，在頒發許可證時，SDK將同時檢查AdobeCRL和您自己的CRL。

要瞭解有關生成CRL的詳細資訊，請參見 `RevocationListFactory` 在 *Adobe訪問API參考*。
