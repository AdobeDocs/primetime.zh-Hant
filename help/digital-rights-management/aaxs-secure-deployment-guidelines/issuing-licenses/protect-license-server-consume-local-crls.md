---
title: 使用本機產生的CRL
description: 使用本機產生的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 使用本地生成的CRL{#consume-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe存取API來驗證簽名。 API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署。

* 請呼叫`RevocationList.verifySignature`以檢查簽名，然後再將RevocationList提供給任何API。

   如需詳細資訊，請參閱&#x200B;*Adobe存取API參考*&#x200B;中的`RevocationListFactory`。

* 在將`PolicyUpdateList`提供給任何API之前，請呼叫`PolicyUpdateList.verifySignature`以檢查簽名。

   如需詳細資訊，請參閱&#x200B;*Adobe存取API參考*&#x200B;中的`PolicyUpdateList`。

