---
title: 授權請求錯誤處理
description: 授權請求錯誤處理
copied-description: true
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 授權請求錯誤處理 {#license-request-error-handling}

如果在請求剖析期間發生錯誤， `HandlerParsingException` 發生。 此例外狀況包含傳回至使用者端的錯誤資訊。 如果您需要擷取錯誤資訊，則需呼叫 `HandlerParsingException.getErrorData()`. 如果由於DRM政策要求未得到滿足而在產生授權期間發生錯誤，則 `PolicyEvaluationException` 發生。 此例外狀況還包括 `ErrorData` 要傳回給使用者端。

請參閱API檔案以瞭解 `LicenseRequestMessage.generateLicense()` 瞭解如何在產生許可證期間評估DRM原則的詳細資訊。
