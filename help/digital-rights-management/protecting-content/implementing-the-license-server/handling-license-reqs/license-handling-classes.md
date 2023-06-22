---
title: 概觀
description: 概觀
copied-description: true
exl-id: 267188d0-83f8-42dc-88e3-78b52945cb6c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 概觀 {#overview}

若要取得授權，使用者端會從內嵌於封裝內容的中繼資料建立請求，然後將該請求提交至授權伺服器。 授權伺服器使用從內容中繼資料擷取的資訊來產生授權。

如果使用者端和伺服器都支援通訊協定版本5，則請求URL為「中繼資料中的授權伺服器URL」+ &quot; [!DNL /flashaccess/license/v4]「。 如果通訊協定版本3是使用者端或伺服器支援的最大值，Primetime DRM使用者端就會傳送驗證請求給「中繼資料中的授權伺服器URL」+ 」 [!DNL /flashaccess/license/v3]「。 否則，驗證請求會傳送到「中繼資料中的授權伺服器URL」+ &quot; [!DNL /flashaccess/license/v1]&quot;

一個裝置可能擁有多個相同內容的授權（相同的授權ID），但只能有一個特定授權ID和DRM原則ID的授權。 如果收到具有重複LicenseID/PolicyID的授權，則只有在新授權的發行日期晚於現有授權的發行日期時，新授權才會取代舊授權。 此邏輯用於處理內嵌於內容中的授權。 因此，不建議在內容區塊中嵌入一個以上使用相同DRM原則ID的授權。 相同的邏輯會套用至透過 `DRMManager.storeVoucher()` ActionScript3 API；如果使用者端已擁有日後發行日期的授權，則提供的授權可能會被忽略。

## 授權請求處理類別 {#section_190E3BEF316C4B09ACC21E4C2BAC5C75}

* `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`  — 這是授權要求處理常式類別。 它會讀取並剖析授權請求。 其 `getRequests()` 方法會傳回以下專案的清單： `LicenseRequestMessage` 物件。
* `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`  — 這是要求訊息類別。 呼叫者應透過 `LicenseRequestMessage` 清單傳回 `getRequests()`，並為每個要求產生授權或設定錯誤代碼。 呼叫 `LicenseRequestMessage.getContentInfo()` 以取得從內容中繼資料擷取的資訊，包括內容ID、授權ID和DRM政策。

授權和錯誤會同時傳送，當 `LicenseHandler.close()` 方法已呼叫。

請參閱 [DRM伺服器API參考檔案](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/overview-summary.html) 以取得詳細資訊。
