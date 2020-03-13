---
seo-title: 授權要求錯誤處理
title: 授權要求錯誤處理
uuid: 4563f546-77fe-4fb9-9ad8-a0689fe6fb4d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 授權要求錯誤處理 {#license-request-error-handling}

如果在請求剖析期間發生錯誤，則會發 `HandlerParsingException` 生。 此例外包括返回給客戶機的錯誤資訊。 如果您需要擷取錯誤資訊，則需要呼叫 `HandlerParsingException.getErrorData()`。 如果由於尚未滿足的DRM策略要求而在生成許可證期間發生錯誤，則會發 `PolicyEvaluationException` 生。 此例外也包 `ErrorData` 括要傳回給用戶端的例外。

如需DRM原則在授權產 `LicenseRequestMessage.generateLicense()` 生期間如何評估的詳細資訊，請參閱API檔案。
