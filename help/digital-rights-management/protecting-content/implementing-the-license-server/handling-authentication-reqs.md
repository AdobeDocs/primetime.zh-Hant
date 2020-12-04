---
seo-title: 處理驗證請求
title: 處理驗證請求
uuid: abcb9cf6-668e-405c-9659-9ed1bcc33024
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 處理驗證請求{#handle-authentication-requests}

`AuthenticationHandler`類用於處理驗證請求。 它僅用於用戶名／密碼驗證。

產生驗證Token時，必須指定Token到期日。 自訂屬性也可能包含在Token中。 如果設定，當驗證Token在後續請求中傳送時，這些屬性會顯示給伺服器。 如需處理自訂驗證Token的相關資訊，請參閱[處理授權要求](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md)。

處理常式會讀取驗證請求，並在呼叫`parseRequest()`時分析請求訊息。 伺服器實作會檢查請求中的使用者憑證，如果憑證有效，則呼叫`getRequest().generateAuthToken()`以產生`AuthenticationToken`物件。 如果`AuthenticationRequestMessage.generateAuthToken()`未在`close()`之前呼叫，則會傳送驗證失敗錯誤碼。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL:+ &quot; [!DNL /flashaccess/authn/v4]&quot;。 如果協定版本3是用戶端或伺服器支援的最高版本，Adobe Primetime DRM用戶端就會傳送驗證要求至「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/authn/v3]」。 否則，驗證請求會傳送至「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/authn/v1]」

