---
title: 處理網域註冊請求
description: 處理網域註冊請求
copied-description: true
exl-id: f846e154-e90c-4e45-aafd-f6e22dac3339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 處理網域註冊請求{#handling-domain-registration-requests}

如果DRM中繼資料指出播放內容需要網域註冊，使用者端應用程式應叫用DRMManager.addToDeviceGroup()ActionScriptAPI或joinLicenseDomain() iOS API。 如果使用者端尚未在指定的網域伺服器註冊（或如果應用程式正在強制重新加入），則會傳送網域註冊要求。 網域伺服器會判斷是否允許使用者端加入網域，並向使用者端發出一或多個網域認證。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的網域伺服器URL： + &quot;/flashaccess/domain/v4」。 否則，請求URL是中繼資料中的網域伺服器URL&quot; + &quot;/flashaccess/domain/v3&quot;

初始化時 `DomainRegistrationHandler`，必須指定網域伺服器URL。 此URL將包含在處理常式發出的網域權杖中，以指出發出權杖的網域伺服器。 該URL必須符合在要求向伺服器註冊網域的任何原則中指定的網域伺服器URL。

若要判斷是否允許使用者端加入網域，伺服器可以檢查要求中的電腦和使用者資訊。 另請參閱 [使用電腦識別碼](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) 瞭解如何識別及計算加入網域的電腦數目。 伺服器也可以決定允許使用者端加入哪個網域。 請注意，使用者端只能是每個網域伺服器URL一個網域的成員。 如果電腦已有此網域伺服器URL的網域權杖，則網域註冊要求將會包含目前的網域名稱( `getRequestDomainName()`)。 對於重新加入請求，網域伺服器必須傳回此網域的目前網域認證集或傳回錯誤（網域伺服器可能不會傳回不同網域的網域認證）。

如果網域伺服器需要驗證才能加入網域，則請求應包含驗證權杖。 就像授權要求一樣，網域註冊可能需要使用者名稱/密碼或自訂驗證。 另請參閱 [使用者驗證](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) 以取得處理驗證Token的詳細資訊。

網域伺服器負責儲存和管理與每個網域相關聯的網域金鑰。 當需要為網域（網域的第一個網域註冊）產生新金鑰組時，叫用 `generateDomainCredential` `(String, int, Principal, Date)`. 此方法將會產生新的網域金鑰組和網域憑證。 網域伺服器必須儲存私密金鑰和憑證，並在處理此網域的後續請求時提供這些物件。 也可以為網域產生新的金鑰組，以便翻轉金鑰。 將滑鼠指向特定網域的金鑰時，請務必增加中的金鑰版本 `generateDomainCredential` 以及。

後續每次機器向相同網域註冊時，都應使用相同的網域私密金鑰和憑證。 叫用 `addDomainCredential(DomainToken, PrivateKey)` 將現有的網域認證傳回使用者端。 如果因為網域金鑰已變更，所以網域有多個網域認證，則伺服器應該提供目前網域金鑰和所有先前網域金鑰的網域認證，讓使用者端可以使用繫結至舊版網域金鑰的授權。 這可讓繫結至舊網域權杖的授權移至新註冊的電腦且仍可播放。
