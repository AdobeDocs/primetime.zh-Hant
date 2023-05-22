---
description: 要使用本地生成的證書吊銷清單(CRL)和策略更新清單，請使用Adobe PrimetimeDRM API驗證簽名。
title: 正在使用本地生成的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 正在使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的證書吊銷清單(CRL)和策略更新清單，請使用Adobe PrimetimeDRM API驗證簽名。

以下API驗證清單是否未被篡改，以及清單是否由正確的許可證伺服器簽名：

* 呼叫 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) 在您提供 [吊銷清單](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 到任何API。

   有關詳細資訊，請參見 [吊銷清單工廠](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 呼叫 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) 在提供 `PolicyUpdateList` 到任何API。

   有關詳細資訊，請參見 [策略更新清單](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

