---
title: 使用者驗證
description: 使用者驗證
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 用戶驗證{#user-authentication}

Adobe存取要求可包含驗證Token。

如果使用使用者名稱／密碼驗證，請求可能包含由`AuthenticationHandler`產生的`AuthenticationToken`。 若要存取並驗證Token，請使用`RequestMessageBase.getAuthenticationToken()`。 若要在用戶端上起始使用者名稱／密碼要求，請使用`DRMManager.authenticate()`ActionScript或iOS API。

如果客戶端和伺服器使用自定義驗證機制，則客戶端通過某些其它通道獲得驗證令牌，並使用`DRMManager.setAuthenticationToken`ActionScript3.0 API設定自定義驗證令牌。 使用`RequestMessageBase.getRawAuthenticationToken()`取得自訂驗證Token。 伺服器實作負責決定自訂驗證Token是否有效。
