---
description: 所有由Adobe Primetime DRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。
seo-description: 所有由Adobe Primetime DRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。
seo-title: 驗證Token的逾時
title: 驗證Token的逾時
uuid: 2c2b0dad-0979-4d49-b109-2700ceb4d722
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc

---


# 驗證Token的逾時{#timeout-for-authentication-tokens}

所有由Adobe Primetime DRM SDK產生的驗證Token都有逾時間隔，以保護應用程式的安全性。

在處理驗證請求時，使用Primetime DRM SDK指定驗證Token的有效期。 Token過期後，此Token即不再有效，使用者必須向授權伺服器再次驗證。

若要進一步瞭解驗證請求，請參 [閱AuthenticationHandler](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。
