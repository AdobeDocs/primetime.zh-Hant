---
title: 用戶驗證
description: 用戶驗證
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# 用戶驗證 {#user-authentication}

Adobe PrimetimeDRM請求可以包含驗證令牌。

如果使用了用戶名/密碼驗證，則請求可能包含 `AuthenticationToken` 由 `AuthenticationHandler`。 如果要訪問並驗證令牌，則需要使用 `RequestMessageBase.getAuthenticationToken()`。 要在客戶端上啟動用戶名/密碼請求，請使用 `DRMManager.authenticate()` ActionScript或iOSAPI。

如果客戶機和伺服器使用自定義認證機制，則客戶機通過其它通道獲得認證令牌並使用 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 獲取自定義身份驗證令牌。 伺服器實現確定自定義驗證令牌是否有效。
