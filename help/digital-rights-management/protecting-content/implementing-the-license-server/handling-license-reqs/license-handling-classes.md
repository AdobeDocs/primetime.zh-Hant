---
title: 概觀
description: 概觀
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 概觀 {#overview}

若要取得授權，使用者端會從內嵌於封裝內容的中繼資料中建立請求，然後將該請求提交至授權伺服器。 許可證伺服器使用從內容中繼資料擷取的資訊來產生許可證。

如果使用者端和伺服器都支援通訊協定版本5，則請求URL為「中繼資料中的授權伺服器URL」+ &quot; [!DNL /flashaccess/license/v4]「。 如果通訊協定版本3是使用者端或伺服器支援的最大值，Primetime DRM使用者端會傳送驗證請求給「中繼資料中的授權伺服器URL」+ 」 [!DNL /flashaccess/license/v3]「。 否則，驗證請求將傳送到「License Server URL in metadata」+ &quot; [!DNL /flashaccess/license/v1]&quot;

一個裝置可以有多個相同內容的授權（相同的授權ID），但只能有一個特定授權ID和DRM政策ID的授權。 如果收到具有重複LicenseID/PolicyID的授權，則只有在新授權的發行日期晚於現有授權的發行日期時，新授權才會取代舊授權。 此邏輯用於處理內嵌於內容中的授權。 因此，不建議在內容區塊中嵌入一個以上具有相同DRM政策ID的授權。 相同的邏輯適用於透過傳遞至使用者端的授權 `DRMManager.storeVoucher()` ActionScript3 API；如果使用者端已擁有日後發行日期的授權，則可能會忽略所提供的授權。

## 授權要求處理類別 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`  — 這是授權要求處理常式類別。 它會讀取並剖析授權請求。 其 `getRequests()` 方法傳回清單 `LicenseRequestMessage` 物件。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`  — 這是要求訊息類別。 呼叫者應透過 `LicenseRequestMessage` 清單傳回 `getRequests()`，並為每項要求產生授權或設定錯誤代碼。 呼叫 `LicenseRequestMessage.getContentInfo()` 以取得從內容中繼資料擷取的資訊，包括內容ID、授權ID和DRM政策。

授權和錯誤會同時傳送，當 `LicenseHandler.close()` 方法稱為。

請參閱 [DRM伺服器API參考檔案](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 以取得詳細資訊。
