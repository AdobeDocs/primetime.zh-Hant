---
title: 處理網域取消註冊請求
description: 處理網域取消註冊請求
copied-description: true
exl-id: f29507b5-d32a-4b22-a02e-6701b86db133
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 處理網域取消註冊請求{#handling-domain-de-registration-requests}

如果使用者端應用程式需要離開網域，它會叫用 `DRMManager.removeFromDeviceGroup()`ActionScriptAPI或 `leaveLicenseDomain()` iOS API可起始網域註銷程式。 網域解除註冊是兩個階段的程式。 使用者端會先傳送取消註冊預覽請求。 網域伺服器會檢查要求，並判斷是否允許使用者端離開網域（如果電腦目前不是網域的一部分，可能會傳回錯誤）。 成功回應後，使用者端會刪除其網域認證及發行給該網域的任何授權，然後傳送取消註冊請求。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的網域伺服器URL： + &quot;/flashaccess/dereg/v4」。 否則，請求URL是中繼資料中的網域伺服器URL&quot; + &quot;/flashaccess/dereg/v3&quot;

處理網域取消註冊請求時，伺服器會使用 `getRequestPhase()` 以判斷使用者端是否處於預覽或取消註冊階段。 在預覽階段中，網域伺服器會檢查要求，並判斷是否允許使用者端離開網域（例如，如果電腦目前不是網域的一部分，則可能會拒絕要求）。 在取消註冊階段，伺服器會記錄電腦已離開網域的事實。 強烈建議伺服器評估預覽請求中的邏輯，與實際取消註冊請求中的邏輯相同，以將第二階段失敗的可能性降至最低。
