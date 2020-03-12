---
description: 若要使用本機產生的憑證撤銷清單(CRL)和政策更新清單，請使用Adobe Primetime DRM API來驗證簽名。
seo-description: 若要使用本機產生的憑證撤銷清單(CRL)和政策更新清單，請使用Adobe Primetime DRM API來驗證簽名。
seo-title: 使用本機產生的CRL
title: 使用本機產生的CRL
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 使用本機產生的CRL {#consuming-locally-generated-crls}

若要使用本機產生的憑證撤銷清單(CRL)和政策更新清單，請使用Adobe Primetime DRM API來驗證簽名。

下列API會確認清單未遭竄改，且清單已由正確的授權伺服器簽署：

* 請呼 [叫RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) ，以在您將 [RevocationList提供給任何API之前檢查簽](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 名。

   如需詳細資訊，請參 [閱RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 在提 [供給任何API之前，請呼叫PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) ，以檢查 `PolicyUpdateList` 簽名。

   如需詳細資訊，請參 [閱PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

