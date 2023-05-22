---
title: 許可證請求錯誤處理
description: 許可證請求錯誤處理
copied-description: true
exl-id: 7cfdebc5-db2b-4629-98e6-31ad71cb424c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---

# 許可證請求錯誤處理 {#license-request-error-handling}

如果在請求分析過程中出錯， `HandlerParsingException` 。 此異常包括返回給客戶端的錯誤資訊。 如果需要檢索錯誤資訊，需要致電 `HandlerParsingException.getErrorData()`。 如果由於未滿足的DRM策略要求而在生成許可證期間出錯， `PolicyEvaluationException` 。 此例外還包括 `ErrorData` 將返回給客戶。

請參閱API文檔， `LicenseRequestMessage.generateLicense()` 有關在許可證生成期間如何評估DRM策略的詳細資訊。
