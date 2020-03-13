---
seo-title: 處理網域註冊請求
title: 處理網域註冊請求
uuid: e0cef9c4-b2d1-4bec-8dce-50452bc826fb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 處理網域註冊請求{#handling-domain-registration-requests}

如果DRM中繼資料指出需要進行網域註冊才能播放內容，用戶端應用程式應叫用DRMManager.addToDeviceGroup()ActionScript API或joinLicenseDomain()iOS API。 如果客戶機尚未向指定的域伺服器註冊（或如果應用程式正在強制重新加入），則會發送域註冊請求。 域伺服器確定是否允許客戶機加入域並向客戶機發出一個或多個域證書。

* 請求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的域伺服器URL:+ &quot;/flashaccess/domain/v4&quot;。 否則，請求URL是中繼資料&quot; + &quot;/flashaccess/domain/v3&quot;中的網域伺服器URL

初始化網 `DomainRegistrationHandler`域伺服器URL時，必須指定網域伺服器URL。 此URL將包含在由處理常式發出的網域Token中，以指出發出Token的網域伺服器。 該URL必須與任何需要向伺服器註冊域的策略中指定的域伺服器URL匹配。

為了確定客戶機是否被允許加入域，伺服器可檢查請求中的電腦和用戶資訊。 有關如 [何識別和計算加入域的電腦](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) ，請參見使用電腦標識符。 伺服器還可以確定允許客戶機加入的域。 請注意，每個網域伺服器URL中，用戶端只能是一個網域的成員。 如果電腦已具有此域伺服器URL的域Token，則域註冊請求將包含當前域名( `getRequestDomainName()`)。 對於重新加入請求，域伺服器必須返回此域的當前組域憑據，或返回錯誤（域伺服器可能不返回不同域的域憑據）。

如果網域伺服器需要驗證才能加入網域，請求應包含驗證Token。 如同授權要求，網域註冊可能需要使用者名稱／密碼或自訂驗證。 如需處 [理驗證Token的詳細資訊](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) ，請參閱使用者驗證。

域伺服器負責儲存和管理與每個域相關聯的域密鑰。 當需要為域生成新的密鑰對（域的第一個域註冊）時，請調用 `generateDomainCredential``(String, int, Principal, Date)`。 此方法將生成新的域密鑰對和域證書。 域伺服器必須儲存私鑰和證書，並在處理此域的後續請求時提供這些對象。 還可以為域生成新的密鑰對，以便滾動到密鑰上。 當滾動到特定域的鍵時，請務必增加鍵版本 `generateDomainCredential` 。

每當電腦註冊到相同域時，應使用相同的域私鑰和證書。 調用 `addDomainCredential(DomainToken, PrivateKey)` 以將現有域憑據返回到客戶端。 如果由於更改了域密鑰而存在多個域憑據，則伺服器應提供當前域密鑰和所有先前域密鑰的域憑據，以便客戶端可以使用綁定到舊域密鑰的許可證。 這可讓系結至舊網域Token的授權移至新註冊的機器，而且仍可播放。
