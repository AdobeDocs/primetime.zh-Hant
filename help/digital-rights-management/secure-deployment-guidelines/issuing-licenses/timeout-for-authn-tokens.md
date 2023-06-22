---
description: Adobe Primetime DRM SDK產生的所有驗證Token都有保護應用程式安全的逾時間隔。
title: 驗證Token逾時
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 驗證Token逾時{#timeout-for-authentication-tokens}

Adobe Primetime DRM SDK產生的所有驗證Token都有保護應用程式安全的逾時間隔。

處理驗證請求時，會使用Primetime DRM SDK指定驗證權杖的到期日。 到期後，權杖不再有效，使用者必須透過授權伺服器再次驗證。

若要進一步瞭解驗證請求，請參閱 [AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html).
