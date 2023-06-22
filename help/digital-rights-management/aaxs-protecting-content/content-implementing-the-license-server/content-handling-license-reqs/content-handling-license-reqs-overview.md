---
title: 概觀
description: 概觀
copied-description: true
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概觀{#overview}

若要請求授權，使用者端會在封裝期間傳送內嵌於內容中的中繼資料。 授權伺服器使用內容中繼資料中的資訊來產生授權。

此 `LicenseHandler` 讀取授權要求並剖析要求。 `LicenseHandler`延伸 `BatchHandlerBase` 以容納批次授權請求，但Adobe存取使用者端目前不支援此功能。 此 `getRequests()` 方法將傳回 `LicenseRequestMessage` 物件。 呼叫者應透過 `LicenseRequestMessages`，並為每個請求產生授權或設定錯誤代碼(請參閱 `LicenseRequestMessage` API參考檔案)。 伺服器會針對每個授權要求，決定是否發行授權。 呼叫 `LicenseRequestMessage.getContentInfo()` 以取得從內容中繼資料擷取的資訊，包括內容ID、授權ID和原則。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的授權伺服器URL： + &quot;/flashaccess/license/v4」。 如果通訊協定版本3是使用者端或伺服器支援的最大版本，則Adobe存取使用者端會傳送驗證請求給「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/license/v3&quot;。 否則，驗證請求會傳送到「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/license/v1&quot;

如果剖析請求時發生錯誤， `HandlerParsingException` 擲回。 此例外狀況包含要傳回至使用者端的錯誤資訊。 若要擷取錯誤資訊，請呼叫 `HandlerParsingException.getErrorData()`. 如果由於不符合原則要求而產生授權時發生錯誤， `PolicyEvaluationException` 擲回。 此例外狀況還包括 `ErrorData` 要傳回給使用者端。 請參閱API檔案以瞭解 `LicenseRequestMessage.generateLicense()` 瞭解在授權產生期間如何評估原則的詳細資訊。

授權和錯誤會在以下情況下同時傳送： `LicenseHandler.close()` 稱為。

一個裝置可能擁有多個相同內容的授權（相同的授權ID），但特定授權ID和原則ID只能有一個授權。 如果收到具有重複LicenseID/PolicyID的授權，則只有在新授權的發行日期晚於現有授權的發行日期時，新授權才會取代舊授權。 此邏輯用於處理內嵌於內容中的授權，因此，不建議在內容區塊中嵌入多個具有相同原則ID的授權。 相同的邏輯會套用至透過 `DRMManager.storeVoucher()` ActionScript3 API；如果使用者端已擁有日後發行日期的授權，則提供的授權可能會被忽略。
