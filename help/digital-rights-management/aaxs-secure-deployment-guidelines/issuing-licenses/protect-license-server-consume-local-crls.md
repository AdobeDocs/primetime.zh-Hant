---
title: 使用本地生成的CRL
description: 使用本地生成的CRL
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 使用本地生成的CRL{#consume-locally-generated-crls}

要使用本地生成的證書吊銷清單(CRL)和策略更新清單，請使用Adobe訪問API驗證簽名。 這些API驗證清單是否未被篡改，以及是否由正確的許可證伺服器簽名。

* 呼叫 `RevocationList.verifySignature` 在向任何API提供RevocationList之前檢查簽名。

   有關詳細資訊，請參見 `RevocationListFactory` 的 *Adobe訪問API參考*。

* 呼叫 `PolicyUpdateList.verifySignature`在提供 `PolicyUpdateList` 到任何API。

   有關詳細資訊，請參見 `PolicyUpdateList` 的 *Adobe訪問API參考*。
