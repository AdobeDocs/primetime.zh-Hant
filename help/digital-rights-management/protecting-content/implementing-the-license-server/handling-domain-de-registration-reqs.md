---
title: 處理網域取消註冊請求
description: 處理網域取消註冊請求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 處理網域取消註冊請求 {#handle-domain-de-registration-requests}

如果使用者端應用程式需要離開網域，則會叫用 `DRMManager.removeFromDeviceGroup()`ActionScriptAPI或 `leaveLicenseDomain()` iOS API會啟動網域取消註冊程式。 網域解除註冊是兩個階段的程式。 使用者端會先傳送取消註冊預覽請求。 網域伺服器會檢查請求，並決定是否允許使用者端離開網域。 如果電腦目前不是網域的一部分，可能會傳回錯誤。 成功回應後，使用者端會刪除其網域認證，以及已核發至該網域的任何授權。 然後它會傳送取消註冊請求。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的網域伺服器URL： + 」 [!DNL /flashaccess/dereg/v4]「。 否則，請求URL是中繼資料中的網域伺服器URL&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

處理網域取消註冊請求時，伺服器會使用 `getRequestPhase()` 以判斷使用者端是否處於預覽或取消註冊階段。 在預覽階段中，網域伺服器會檢查要求，並決定是否允許使用者端離開網域，因為要求可能會被拒絕；例如，如果電腦目前不是網域的一部分，要求可能會被拒絕。 在取消註冊階段，伺服器會記錄電腦已離開網域的事實。 強烈建議伺服器評估預覽請求中的邏輯，與實際取消註冊請求中的邏輯相同，以將第二階段失敗的可能性降至最低。
