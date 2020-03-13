---
seo-title: 使用者驗證
title: 使用者驗證
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用者驗證{#user-authentication}

Adobe Access要求可包含驗證Token。

如果使用使用者名稱／密碼驗證，請求可能包含由 `AuthenticationToken` 產生的 `AuthenticationHandler`。 若要存取並驗證Token，請使用 `RequestMessageBase.getAuthenticationToken()`。 若要在用戶端上起始使用者名稱／密碼要求，請使 `DRMManager.authenticate()` 用ActionScript或iOS API。

如果用戶端和伺服器使用自訂驗證機制，用戶端會透過其他通道取得驗證Token，並使用 `DRMManager.setAuthenticationToken` ActionScript 3.0 API設定自訂驗證Token。 使用 `RequestMessageBase.getRawAuthenticationToken()` 取得自訂驗證Token。 伺服器實作負責決定自訂驗證Token是否有效。
