---
seo-title: 處理驗證請求
title: 處理驗證請求
uuid: 036582d4-611c-4772-b247-81a3144fd5d6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 處理驗證請求{#handling-authentication-requests}

該類 `AuthenticationHandler` 用於處理驗證請求。 它僅用於用戶名／密碼驗證。

產生驗證Token時，必須指定Token到期日。 自訂屬性也可能包含在Token中。 如果設定，當驗證Token在後續請求中傳送時，這些屬性會顯示給伺服器。 如需處 [理自訂驗證Token的相關資訊](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) ，請參閱處理授權要求。

處理常式會讀取驗證請求，並在呼叫時解析請 `parseRequest()` 求訊息。 伺服器實作會檢查請求中的使用者認證，如果認證有效，則會呼叫 `AuthenticationToken` 以產生物件 `getRequest().generateAuthToken()`。 如果 `AuthenticationRequestMessage.generateAuthToken()` 之前未呼叫， `close()`則會傳送驗證失敗錯誤碼。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL:+ &quot;/flashaccess/authn/v4&quot;。 如果用戶端或伺服器支援的通訊協定版本3是最高版本，Adobe Access用戶端會傳送驗證要求至「中繼資料中的授權伺服器URL」+「/flashaccess/authn/v3」。 否則，驗證要求會傳送至「中繼資料中的授權伺服器URL」+「/flashaccess/authn/v1」

