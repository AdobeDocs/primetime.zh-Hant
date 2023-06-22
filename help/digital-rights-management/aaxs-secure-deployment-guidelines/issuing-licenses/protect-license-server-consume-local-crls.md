---
title: 使用本機產生的CRL
description: 使用本機產生的CRL
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 使用本機產生的CRL{#consume-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe存取API來驗證簽章。 API會確認清單未被竄改，且已透過正確的License Server簽署。

* 呼叫 `RevocationList.verifySignature` 在將RevocationList提供給任何API之前檢查簽章。

   如需詳細資訊，請參閱 `RevocationListFactory` 在 *Adobe存取API參考*.

* 呼叫 `PolicyUpdateList.verifySignature`以在提供 `PolicyUpdateList` 至任何API。

   如需詳細資訊，請參閱 `PolicyUpdateList` 在 *Adobe存取API參考*.
