---
title: 處理域註冊請求
description: 處理域註冊請求
copied-description: true
exl-id: 6f4ed908-32ee-4c8b-8965-53381b737989
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 處理域註冊請求 {#handle-domain-registration-requests}

如果DRM元資料指示需要域註冊來播放內容，則客戶端應用程式應調用 `DRMManager.addToDeviceGroup()` ActionScriptAPI或 `joinLicenseDomain()` iOSAPI 如果客戶端尚未向指定的域伺服器註冊（或如果應用程式正在強制重新加入），則發送域註冊請求。 域伺服器確定是否允許客戶機加入域並向客戶機發出一個或多個域憑據。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，則請求URL為「元資料中的域伺服器URL:+ &quot; [!DNL /flashaccess/domain/v4]。 否則，請求URL為元資料&quot;+ &quot;中的域伺服器URL [!DNL /flashaccess/domain/v3]&quot;

初始化時 `DomainRegistrationHandler`，必須指定域伺服器URL。 然後，此URL包含在由處理程式發出的域令牌中，以向域伺服器指示令牌已發出。 該URL必須與任何需要向伺服器註冊域的DRM策略中指定的域伺服器URL匹配。

為了確定是否允許客戶機加入域，伺服器可以檢查請求中的機器和用戶資訊。 伺服器還可以確定允許客戶機加入的域。

>[!NOTE]
>
>客戶端只能是每個域伺服器URL的一個域的成員。 如果電腦已具有此域伺服器URL的域令牌，則域註冊請求包括當前域名( `getRequestDomainName()`)。

對於重新加入請求，域伺服器必須返回此域的當前域憑據集或返回錯誤。 域伺服器不能返回其他域的域憑據。

請參閱 [使用電腦標識符](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers) 有關如何識別和計數加入域的電腦的資訊。

如果域伺服器需要身份驗證才能加入域，則請求應包含身份驗證令牌。 與許可證請求一樣，域註冊可能需要用戶名/密碼或自定義身份驗證。

請參閱 [用戶驗證](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication) 以獲取有關如何管理身份驗證令牌的詳細資訊。

域伺服器負責儲存和管理與每個域關聯的域密鑰。 當需要為域生成新密鑰對（域的第一個域註冊）時，需要調用 `generateDomainCredential(String, int, Principal, Date)`。 該方法生成新的域密鑰對和域證書。 域伺服器必須儲存私鑰和證書，並在處理此域的後續請求時提供這些對象。 還可以為域生成新密鑰對，以便滾過密鑰。 滾動到特定域的鍵時，請確保在 `generateDomainCredential`。

每次電腦在同一域註冊後，都應使用相同的域私鑰和證書。 調用 `addDomainCredential(DomainToken, PrivateKey)` 將現有域憑據返回到客戶端。 如果由於更改了域密鑰而存在該域的多個域憑據，則伺服器應提供當前域密鑰和所有先前域密鑰的域憑據，以便客戶端可以使用綁定到較舊域密鑰的許可證。 這樣，綁定到舊域令牌的許可證就可以移動到新註冊的電腦，並且仍然可以播放。
