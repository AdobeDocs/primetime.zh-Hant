---
title: 概述
description: 概述
copied-description: true
exl-id: f1a55d5c-c7df-4b8f-8c1e-875d30026069
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概述{#overview}

為請求許可證，客戶端在打包期間發送嵌入內容中的元資料。 許可證伺服器使用內容元資料中的資訊來生成許可證。

的 `LicenseHandler` 讀取許可證請求並解析該請求。 `LicenseHandler`延伸 `BatchHandlerBase` 以容納批許可請求，儘管Adobe訪問客戶端當前不支援此功能。 的 `getRequests()` 方法將返回 `LicenseRequestMessage` 對象。 調用方應迭代 `LicenseRequestMessages`，並針對每個請求生成許可證或設定錯誤代碼(請參見 `LicenseRequestMessage` API參考文檔（瞭解詳細資訊）。 對於每個許可請求，伺服器確定它是否將頒發許可。 呼叫 `LicenseRequestMessage.getContentInfo()` 從內容元資料（包括內容ID、許可ID和策略）中獲取資訊。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.license.LicenseHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.license.LicenseRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，請求URL為「元資料中的許可證伺服器URL:+「/flashaccess/license/v4」。 如果客戶端或伺服器支援的協定版本3是最大版本，則Adobe訪問客戶端將向「元資料中的許可證伺服器URL」+「/flashaccess/license/v3」發送身份驗證請求。 否則，身份驗證請求將發送到「元資料中的許可證伺服器URL」+「/flashaccess/license/v1」

如果分析請求時出錯， `HandlerParsingException` 。 此異常包含要返回給客戶端的錯誤資訊。 要檢索錯誤資訊，請調用 `HandlerParsingException.getErrorData()`。 如果由於未滿足策略要求而生成許可證時出錯， `PolicyEvaluationException` 。 此例外還包括 `ErrorData` 將返回給客戶。 請參閱API文檔， `LicenseRequestMessage.generateLicense()` 有關在許可證生成過程中如何評估策略的詳細資訊。

許可證和錯誤在 `LicenseHandler.close()` 。

設備可以具有多個相同內容的許可證（相同的許可證ID），但只能具有一個特定許可證ID和策略ID的許可證。 如果它收到具有重複的許可證ID/策略ID的許可證，則僅當新許可證的頒發日期晚於現有許可證的頒發日期時，新許可證才會替換舊許可證。 此邏輯用於處理嵌入到內容中的許可證，因此，建議不要在內容塊中嵌入多個具有相同策略ID的許可證。 同樣的邏輯適用於通過 `DRMManager.storeVoucher()` ActionScript3 API;如果客戶端已經擁有具有稍後發放日期的許可證，則可忽略提供的許可證。
