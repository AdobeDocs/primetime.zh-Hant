---
title: 用戶驗證
description: 用戶驗證
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 用戶驗證{#user-authentication}

Adobe訪問請求可以包含驗證令牌。

如果使用了用戶名/密碼身份驗證，則請求可能包含 `AuthenticationToken` 由 `AuthenticationHandler`。 要訪問和驗證令牌，請使用 `RequestMessageBase.getAuthenticationToken()`。 要在客戶端上啟動用戶名/密碼請求，請使用 `DRMManager.authenticate()` ActionScript或iOSAPI。

如果客戶端和伺服器使用定制認證機制，則客戶端通過其它通道獲得認證令牌並使用 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 獲取自定義身份驗證令牌。 伺服器實現負責確定自定義驗證令牌是否有效。
