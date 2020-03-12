---
seo-title: 產生CRL以補充Adobe發佈的CRL
title: 產生CRL以補充Adobe發佈的CRL
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 產生CRL以補充Adobe發佈的CRL{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access可讓您建立CRL，以補充Adobe發佈的機器CRL。 Adobe Access SDK會檢查並強制執行Adobe CRL，但您可以建立廢止其他電腦憑證的CRL，以禁止其他用戶端電腦。 若要這麼做，您必須將CRL傳遞至Adobe Access SDK，然後，在核發授權時，SDK會檢查Adobe CRL和您自己的CRL。

如需有關產生CRL的詳細資訊，請參 `RevocationListFactory` 閱 *Adobe Access API參考*。
