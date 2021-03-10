---
description: 所有由Adobe PrimetimeDRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。
title: 驗證Token的逾時
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 驗證Token的逾時{#timeout-for-authentication-tokens}

所有由Adobe PrimetimeDRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。

在處理驗證請求時，使用Primetime DRM SDK指定驗證Token的有效期。 Token過期後，此Token即不再有效，使用者必須向授權伺服器再次驗證。

若要進一步瞭解驗證請求，請參閱[AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。
