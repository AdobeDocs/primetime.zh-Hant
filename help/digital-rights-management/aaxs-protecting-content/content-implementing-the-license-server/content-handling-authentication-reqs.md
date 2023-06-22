---
title: 處理驗證請求
description: 處理驗證請求
copied-description: true
exl-id: c1d46ec0-e053-4824-b3b1-20320e259fbe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 處理驗證請求{#handling-authentication-requests}

此 `AuthenticationHandler` 類別用於處理驗證請求。 它僅用於使用者名稱/密碼驗證。

產生驗證Token時，必須指定Token到期日。 Token中也可能包含自訂屬性。 如果設定，在後續請求中傳送驗證Token時，伺服器將可看見這些屬性。 另請參閱 [處理授權請求](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) 以取得有關處理自訂驗證Token的資訊。

處理常式會讀取驗證要求，並剖析要求訊息，當 `parseRequest()` 稱為。 伺服器實作會檢查請求中的使用者認證，如果認證有效，則產生 `AuthenticationToken` 物件，透過呼叫 `getRequest().generateAuthToken()`. 若 `AuthenticationRequestMessage.generateAuthToken()` 之前未呼叫 `close()`，則會傳送驗證失敗錯誤代碼。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的授權伺服器URL： + &quot;/flashaccess/authn/v4」。 如果通訊協定版本3是使用者端或伺服器支援的最大版本，則Adobe存取使用者端會傳送驗證請求給「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/authn/v3&quot;。 否則，驗證請求會傳送到「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/authn/v1&quot;
