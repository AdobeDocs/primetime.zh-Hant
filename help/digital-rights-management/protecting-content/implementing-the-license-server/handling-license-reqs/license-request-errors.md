---
title: 授權請求錯誤處理
description: 授權請求錯誤處理
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 授權請求錯誤處理 {#license-request-error-handling}

如果在剖析請求時發生錯誤， `HandlerParsingException` 發生。 此例外狀況包含傳回給使用者端的錯誤資訊。 如果您需要擷取錯誤資訊，則需呼叫 `HandlerParsingException.getErrorData()`. 如果因為DRM政策要求未得到滿足而在產生授權期間發生錯誤，則 `PolicyEvaluationException` 發生。 此例外狀況還包括 `ErrorData` 要傳回給使用者端。

請參閱API檔案以瞭解 `LicenseRequestMessage.generateLicense()` 瞭解如何在產生許可證期間評估DRM政策的詳細資訊。
