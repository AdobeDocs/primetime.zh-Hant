---
title: 處理身份驗證請求
description: 處理身份驗證請求
copied-description: true
exl-id: 64d23db0-254d-46b1-8317-ba0381509b44
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 處理身份驗證請求 {#handle-authentication-requests}

的 `AuthenticationHandler` 類用於處理身份驗證請求。 它僅用於用戶名/密碼驗證。

生成驗證令牌時，必須指定令牌到期日期。 自定義屬性也可包括在令牌中。 如果設定，則當在後續請求中發送驗證令牌時，伺服器將可以看到這些屬性。 請參閱 [處理許可證請求](../../protecting-content/implementing-the-license-server/handling-license-reqs/license-handling-classes.md) 有關處理自定義身份驗證令牌的資訊。

處理程式讀取驗證請求並解析請求消息 `parseRequest()` 。 伺服器實現會檢查請求中的用戶憑據，如果憑據有效，則生成 `AuthenticationToken` 調用對象 `getRequest().generateAuthToken()`。 如果 `AuthenticationRequestMessage.generateAuthToken()` 未調用之前 `close()`，將發送驗證失敗錯誤代碼。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，請求URL為「元資料中的許可證伺服器URL:+ &quot; [!DNL /flashaccess/authn/v4]。 如果客戶端或伺服器支援的協定版本3是最大版本，則Adobe PrimetimeDRM客戶端將身份驗證請求發送到「元資料中的許可證伺服器URL」+ &quot; [!DNL /flashaccess/authn/v3]。 否則，身份驗證請求將發送到「元資料中的許可證伺服器URL」+ &quot; [!DNL /flashaccess/authn/v1]&quot;
