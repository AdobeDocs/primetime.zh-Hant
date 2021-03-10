---
title: 處理網域註冊請求
description: 處理網域註冊請求
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---


# 處理域註冊請求{#handle-domain-registration-requests}

如果DRM元資料指示需要域註冊才能播放內容，則客戶端應用程式應調用`DRMManager.addToDeviceGroup()`ActionScriptAPI或`joinLicenseDomain()` iOS API。 如果客戶機尚未向指定的域伺服器註冊（或如果應用程式正在強制重新加入），則會發送域註冊請求。 域伺服器確定是否允許客戶機加入域並向客戶機發出一個或多個域證書。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的域伺服器URL:+ &quot; [!DNL /flashaccess/domain/v4]&quot;。 否則，請求URL是中繼資料中的網域伺服器URL&quot; + &quot; [!DNL /flashaccess/domain/v3]&quot;

初始化`DomainRegistrationHandler`時，必須指定域伺服器URL。 然後，此URL會包含在由處理常式發出的網域Token中，以向網域伺服器指出Token已發出。 該URL必須與任何需要向伺服器註冊域的DRM策略中指定的域伺服器URL匹配。

為了確定客戶機是否被允許加入域，伺服器可檢查請求中的電腦和用戶資訊。 伺服器還可以確定允許客戶機加入的域。

>[!NOTE]
>
>每個域伺服器URL中，客戶端只能是一個域的成員。 如果電腦已具有此域伺服器URL的域Token，則域註冊請求包括當前域名(`getRequestDomainName()`)。

對於重新加入請求，域伺服器必須返回此域的當前一組域憑據，或返回錯誤。 域伺服器不能返回不同域的域憑據。

有關如何識別和計算加入域的電腦的資訊，請參見[使用電腦標識符](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#use-machine-identifiers)。

如果網域伺服器需要驗證才能加入網域，請求應包含驗證Token。 如同授權要求，網域註冊可能需要使用者名稱／密碼或自訂驗證。

如需如何管理驗證Token的詳細資訊，請參閱[使用者驗證](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#user-authentication)。

域伺服器負責儲存和管理與每個域相關聯的域密鑰。 當需要為域生成新的密鑰對（域的第一個域註冊）時，需要調用`generateDomainCredential(String, int, Principal, Date)`。 該方法生成新的域密鑰對和域證書。 域伺服器必須儲存私鑰和證書，並在處理此域的後續請求時提供這些對象。 還可以為域生成新的密鑰對，以便滾動到密鑰上。 將滑鼠指針置於特定域的鍵上時，請務必在`generateDomainCredential`中增加鍵版本。

每當機器在相同網域註冊時，應使用相同的網域私密金鑰和憑證。 調用`addDomainCredential(DomainToken, PrivateKey)`將現有域憑據返回到客戶端。 如果由於更改了域密鑰而存在多個域憑據，則伺服器應提供當前域密鑰和所有先前域密鑰的域憑據，以便客戶端可以使用綁定到舊域密鑰的許可證。 這可讓系結至舊網域Token的授權移至新註冊的機器，而且仍可播放。
