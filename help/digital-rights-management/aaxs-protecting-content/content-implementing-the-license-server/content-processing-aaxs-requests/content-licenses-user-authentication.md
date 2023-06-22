---
title: 使用者驗證
description: 使用者驗證
copied-description: true
exl-id: a0dd7d81-2249-4845-94da-53b755d6cd7c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 使用者驗證{#user-authentication}

Adobe存取請求可包含驗證權杖。

如果使用使用者名稱/密碼驗證，請求可能包含 `AuthenticationToken` 產生者： `AuthenticationHandler`. 若要存取及驗證Token，請使用 `RequestMessageBase.getAuthenticationToken()`. 若要在使用者端上起始使用者名稱/密碼請求，請使用 `DRMManager.authenticate()` ActionScript或iOS API。

如果使用者端和伺服器使用自訂驗證機制，使用者端會透過其他通道取得驗證權杖，並使用設定自訂驗證權杖 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 以取得自訂驗證Token。 伺服器實作負責判斷自訂驗證權杖是否有效。
