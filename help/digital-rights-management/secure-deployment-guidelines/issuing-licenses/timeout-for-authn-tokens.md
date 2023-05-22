---
description: 由Adobe PrimetimeDRM SDK生成的所有驗證令牌都有一個超時間隔，以保護應用程式安全。
title: 驗證令牌超時
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# 驗證令牌超時{#timeout-for-authentication-tokens}

由Adobe PrimetimeDRM SDK生成的所有驗證令牌都有一個超時間隔，以保護應用程式安全。

在處理驗證請求時，使用黃金時段DRM SDK指定驗證令牌的過期。 在令牌過期後，該令牌不再有效，用戶必須向許可證伺服器再次進行身份驗證。

要瞭解有關身份驗證請求的詳細資訊，請參見 [驗證處理程式](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/authentication/AuthenticationHandler.html)。
