---
seo-title: 廢止DRM用戶端和執行時期認證
title: 廢止DRM用戶端和執行時期認證
uuid: 8e36536a-8eed-4d27-8a5f-8d3219817e57
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 廢止DRM用戶端和執行時期認證 {#revoking-drm-client-and-runtime-credentials}

DRM/Runtime版本由安全級別、版本號和其他屬性（包括作業系統和運行時）來識別。 要限制允許的DRM/運行時版本，請在DRM策略或中設定模組限制 `HandlerConfiguration`。 模組限制可以包括最低安全級別和不允許頒發許可證的模組版本清單。

有關用 [於標識DRM/Runtime模組的屬性的詳細資訊](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blacklist-drm-clients.md) ，請參閱限制訪問受保護內容的DRM客戶機黑名單。

如果已設定最低安全等級，用戶端上的版本（在機器Token中指定）必須大於或等於指定值。

如果指定了已排除版本的清單，並且客戶機的版本與清單中的任何版本標識符匹配，則客戶機將不允許使用包含此ModuleRequirements實例的權限。 對於模組，如果要匹配版本資訊，則版本資訊中指定的所有參數（版本除外）必須完全匹配模組的值。 如果客戶端模組的值小於或等於版本資訊中的值，則版本版本匹配。

當特定DRM用戶端或執行時期版本報告有違規情事時，內容擁有者和內容分發者（執行授權伺服器）可設定伺服器在Adobe無法修正的期間拒絕發行授權。 這可以通過上述 `HandlerConfiguration` 配置，或通過更改所有DRM策略來配置。 在後一種情況下，您可以維護DRM策略更新清單，並使用該清單檢查DRM策略是否已更新或已撤銷。

如果您需要較新版本的Adobe Flash Player/Adobe AIR Runtime或Adobe內容保護程式庫（DRM模組），則需要更新您的DRM政策。

請參 [閱使用Java API更新原則](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md)。

然後，您需要建立DRM策略更新清單或通過調用或 `HandlerConfiguration` 在中設定 `HandlerConfiguration.setRuntimeModuleRequirements()` 限制 `HandlerConfiguration.setDRMModuleRequirements()`。 當使用者要求啟用指定黑名單的新授權時，您必須先安裝最新的執行階段和程式庫，才能核發授權。

請參閱使用Java API更 [新原則中的范常式式碼。如需黑名單DRM和執行時期版本的範例](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) ，請參閱黑名單DRM和執行時期版本的範例。
