---
title: 授權要求錯誤處理
description: 授權要求錯誤處理
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 0%

---


# 處理{#license-request-error-handling}授權要求錯誤

如果在請求剖析期間發生錯誤，則會發生`HandlerParsingException`。 此例外包括返回給客戶機的錯誤資訊。 如果需要檢索錯誤資訊，則需要調用`HandlerParsingException.getErrorData()`。 如果由於尚未滿足的DRM策略要求而在生成許可證期間發生錯誤，則出現`PolicyEvaluationException`。 此例外還包括要返回到客戶機的`ErrorData`。

請參閱`LicenseRequestMessage.generateLicense()`的API檔案，以取得有關在授權產生期間如何評估DRM原則的詳細資訊。
