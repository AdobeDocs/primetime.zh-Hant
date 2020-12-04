---
seo-title: 使用本機產生的CRL
title: 使用本機產生的CRL
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 使用本地生成的CRL{#consume-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe Access API來驗證簽名。 API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署。

* 請呼叫`RevocationList.verifySignature`以檢查簽名，然後再將RevocationList提供給任何API。

   如需詳細資訊，請參閱&#x200B;*Adobe Access API Reference*&#x200B;中的`RevocationListFactory`。

* 在將`PolicyUpdateList`提供給任何API之前，請呼叫`PolicyUpdateList.verifySignature`以檢查簽名。

   如需詳細資訊，請參閱&#x200B;*Adobe Access API Reference*&#x200B;中的`PolicyUpdateList`。

