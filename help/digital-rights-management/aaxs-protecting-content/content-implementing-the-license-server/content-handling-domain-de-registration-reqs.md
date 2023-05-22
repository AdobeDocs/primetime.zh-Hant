---
title: 處理域取消註冊請求
description: 處理域取消註冊請求
copied-description: true
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 處理域取消註冊請求{#handling-domain-de-registration-requests}

如果客戶端應用程式需要離開域，則調用 `DRMManager.removeFromDeviceGroup()`ActionScriptAPI或 `leaveLicenseDomain()` iOSAPI啟動域註銷進程。 域去註冊是一個兩階段的過程。 客戶端首先發送取消註冊預覽請求。 域伺服器檢查請求並確定是否允許客戶端離開域（如果電腦當前不是域的一部分，則可能返回錯誤）。 在成功響應時，客戶端刪除其域憑據和頒發給該域的任何許可證，然後發送取消註冊請求。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，則請求URL為「元資料中的域伺服器URL:+ &quot;/flashaccess/dereg/v4&quot;。 否則，請求URL為元資料中的域伺服器URL&quot;+ &quot;/flashaccess/dereg/v3&quot;

處理域註銷請求時，伺服器使用 `getRequestPhase()` 確定客戶端是否處於預覽或取消註冊階段。 在預覽階段，域伺服器檢查該請求並確定是否允許客戶端離開該域（例如，如果電腦當前不是域的一部分，則可以拒絕該請求）。 在取消註冊階段，伺服器記錄電腦已離開域的事實。 強烈建議伺服器評估預覽請求中與實際取消註冊請求中相同的邏輯，以最小化第二階段失敗的可能性。
