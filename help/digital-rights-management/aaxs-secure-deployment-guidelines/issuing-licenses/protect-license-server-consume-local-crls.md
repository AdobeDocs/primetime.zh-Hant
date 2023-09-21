---
title: 使用本機產生的CRL
description: 使用本機產生的CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 使用本機產生的CRL{#consume-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe存取API來驗證簽章。 API會確認清單是否未被竄改，而且是由正確的License Server簽署。

* 呼叫 `RevocationList.verifySignature` 在將RevocationList提供給任何API之前檢查簽章。

  如需詳細資訊，請參閱 `RevocationListFactory` 在 *Adobe存取API參考*.

* 呼叫 `PolicyUpdateList.verifySignature`以在提供 `PolicyUpdateList` 至任何API。

  如需詳細資訊，請參閱 `PolicyUpdateList` 在 *Adobe存取API參考*.
