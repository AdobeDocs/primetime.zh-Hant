---
seo-title: 使用者驗證
title: 使用者驗證
uuid: 191964eb-cd68-47a6-8214-aec01f993df4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 用戶驗證{#user-authentication}

Adobe Access要求可包含驗證Token。

如果使用使用者名稱／密碼驗證，請求可能包含由`AuthenticationHandler`產生的`AuthenticationToken`。 若要存取並驗證Token，請使用`RequestMessageBase.getAuthenticationToken()`。 若要在用戶端上起始使用者名稱／密碼要求，請使用`DRMManager.authenticate()` ActionScript或iOS API。

如果客戶端和伺服器使用自訂驗證機制，則客戶端通過某些其他通道獲得驗證令牌，並使用`DRMManager.setAuthenticationToken` ActionScript 3.0 API設定自訂驗證令牌。 使用`RequestMessageBase.getRawAuthenticationToken()`取得自訂驗證Token。 伺服器實作負責決定自訂驗證Token是否有效。
