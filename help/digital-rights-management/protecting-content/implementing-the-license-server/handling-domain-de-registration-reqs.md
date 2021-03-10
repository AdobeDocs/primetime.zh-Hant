---
title: 處理網域取消註冊請求
description: 處理網域取消註冊請求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 處理域取消註冊請求{#handle-domain-de-registration-requests}

如果客戶端應用程式需要離開域，則會調用`DRMManager.removeFromDeviceGroup()`ActionScriptAPI或`leaveLicenseDomain()` iOS API來啟動域取消註冊過程。 域去配準是一個兩階段的過程。 用戶端首先傳送取消註冊預覽請求。 網域伺服器會檢查請求並判斷用戶端是否獲准離開網域。 如果電腦當前不屬於域，則可能返回錯誤。 在成功回應時，用戶端會刪除其網域憑證和已核發至該網域的任何授權。 然後會傳送取消註冊請求。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.domain.DomainDeRegistrationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的域伺服器URL:+ &quot; [!DNL /flashaccess/dereg/v4]&quot;。 否則，請求URL是中繼資料中的網域伺服器URL&quot; + &quot; [!DNL /flashaccess/dereg/v3]&quot;

處理域取消註冊請求時，伺服器使用`getRequestPhase()`來確定客戶端是處於預覽階段還是取消註冊階段。 在預覽階段，網域伺服器會檢查請求，並判斷用戶端是否允許離開網域，因為請求可能遭拒；例如，如果電腦當前不屬於域，則可能拒絕請求。 在取消註冊階段，伺服器記錄電腦已離開域的事實。 強烈建議伺服器在預覽請求中評估與實際取消註冊請求中相同的邏輯，以將第二階段失敗的可能性降至最低。
