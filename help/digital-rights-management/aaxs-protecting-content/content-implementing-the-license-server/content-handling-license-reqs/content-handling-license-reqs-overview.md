---
title: 概觀
description: 概觀
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 概述{#overview}

為請求授權，用戶端會傳送封裝期間內嵌在內容中的中繼資料。 授權伺服器使用內容中繼資料中的資訊來產生授權。

`LicenseHandler`會讀取授權要求並分析該要求。 `LicenseHandler`擴充 `BatchHandlerBase` 功能以容納批次授權要求，不過Adobe存取用戶端目前不支援此功能。`getRequests()`方法將返回`LicenseRequestMessage`對象的清單。 呼叫者應重複`LicenseRequestMessages`，而針對每個請求，請產生授權或設定錯誤碼（如需詳細資訊，請參閱`LicenseRequestMessage` API參考檔案）。 對於每個授權要求，伺服器會決定是否要發行授權。 呼叫`LicenseRequestMessage.getContentInfo()`以取得從內容中繼資料擷取的資訊，包括內容ID、授權ID和原則。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL:+ &quot;/flashaccess/license/v4&quot;。 如果客戶端或伺服器支援的協定版本3是最大版本，Adobe訪問客戶端將向「元資料中的許可證伺服器URL」+ &quot;/flashaccess/license/v3&quot;發送驗證請求。 否則，驗證要求會傳送至「中繼資料中的授權伺服器URL」+「/flashaccess/license/v1」

如果解析請求時發生錯誤，則會拋出`HandlerParsingException`。 此例外包含要返回給客戶機的錯誤資訊。 要檢索錯誤資訊，請調用`HandlerParsingException.getErrorData()`。 如果由於未滿足策略要求而生成許可證時出錯，則拋出`PolicyEvaluationException`。 此例外還包括要返回到客戶機的`ErrorData`。 請參閱`LicenseRequestMessage.generateLicense()`的API檔案，以取得授權產生期間如何評估原則的詳細資訊。

呼叫`LicenseHandler.close()`時，會一次傳送授權和錯誤。

裝置可針對相同內容（相同的授權ID）擁有多份授權，但特定授權ID和原則ID只能有一份授權。 如果收到具有重複LicenseID/PolicyID的授權，則新授權只有在新授權的發行日期晚於現有授權的發行日期時，才會取代舊授權。 此邏輯用於處理內嵌在內容中的授權，因此建議不要在內容區塊中嵌入多個具有相同原則ID的授權。 同樣的邏輯適用於透過`DRMManager.storeVoucher()`ActionScript3 API傳遞給用戶端的授權；如果用戶端已擁有授權，且日後發行日期已過，則可能會忽略所提供的授權。
