---
seo-title: 使用本機產生的CRL
title: 使用本機產生的CRL
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用本機產生的CRL{#consume-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe Access API來驗證簽名。 API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署。

* 在將 `RevocationList.verifySignature` RevocationList提供給任何API之前，請呼叫檢查簽名。

   如需詳細資訊，請 `RevocationListFactory` 參閱 *Adobe Access API參考*。

* 在提 `PolicyUpdateList.verifySignature`供給任何API之前，請呼叫 `PolicyUpdateList` 檢查簽名。

   如需詳細資訊，請 `PolicyUpdateList` 參閱 *Adobe Access API參考*。

