---
seo-title: 廢止DRM用戶端和執行時期認證
title: 廢止DRM用戶端和執行時期認證
uuid: 774b8ac7-51bb-42fc-a05d-cfa718e24a81
translation-type: tm+mt
source-git-commit: fbc175f383c850a7286b1e6e89daa027e00b29ef
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# 廢止DRM用戶端和執行階段認證{#revoking-drm-client-and-runtime-credentials}

DRM/Runtime版本由安全級別、版本號和其他屬性（包括OS和運行時）來識別。 若要限制允許的DRM/Runtime版本，請在原則或`HandlerConfiguration`中設定模組限制。 模組限制可以包括最低安全級別和不允許頒發許可證的模組版本清單。 有關用於標識DRM/Runtime模組的屬性的詳細資訊，請參見[限制訪問受保護內容的DRM客戶端的塊清單](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md)。

如果已設定最低安全等級，用戶端上的版本（在機器Token中指定）必須大於或等於指定值。

如果指定了已排除版本的清單，並且客戶機的版本與清單中的任何版本標識符匹配，則客戶機將不允許使用包含此ModuleRequirements實例的權限。 對於模組，如果要匹配版本資訊，則版本資訊中指定的所有參數（版本除外）必須完全匹配模組的值。 如果客戶端模組的值小於或等於版本資訊中的值，則版本版本匹配。

當特定DRM用戶端或執行時期版本報告有違規情事時，內容擁有者和內容分發者（執行授權伺服器）可設定伺服器在Adobe無法修正的期間拒絕發行授權。 這可以通過`HandlerConfiguration`進行配置（如上所述），或通過更改所有策略進行配置。 在後一種情況下，您可以維護策略更新清單，並使用它檢查策略是否已更新或已撤銷。

如果您需要較新版本的Adobe® Flash® Player/Adobe® AIR® Runtime或Adobe Content Protection程式庫（DRM模組），請依照[使用Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)更新原則並建立原則更新清單，或透過叫用`HandlerConfiguration.setRuntimeModuleRequirements()`或&lt;a4在`HandlerConfiguration`中設定限制/>。 `HandlerConfiguration.setDRMModuleRequirements()`當使用者要求啟用這些區塊清單的新授權時，必須先安裝較新的執行階段和程式庫，才能核發授權。 有關列出DRM和運行時版本的塊的示例，請參見[使用Java API](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)更新策略中的示例代碼。
