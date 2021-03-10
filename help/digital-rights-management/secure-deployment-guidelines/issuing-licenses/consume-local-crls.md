---
description: 若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe PrimetimeDRM API來驗證簽名。
title: 使用本機產生的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 使用本地生成的CRL {#consuming-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和原則更新清單，請使用Adobe PrimetimeDRM API來驗證簽名。

下列API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署：

* 在您將[RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html)提供給任何API之前，請呼叫[RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate))以檢查簽名。

   如需詳細資訊，請參閱[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 在將`PolicyUpdateList`提供給任何API之前，請呼叫[PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate))以檢查簽名。

   如需詳細資訊，請參閱[PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

