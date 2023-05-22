---
title: 撤消DRM客戶端和運行時憑據
description: 撤消DRM客戶端和運行時憑據
copied-description: true
exl-id: f39d6523-9215-49ec-bb3b-e60fe6690dca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 撤消DRM客戶端和運行時憑據{#revoking-drm-client-and-runtime-credentials}

DRM/運行時版本由安全級別、版本號和包括OS和運行時在內的其他屬性標識。 要限制允許的DRM/運行時版本，請在策略或 `HandlerConfiguration`。 模組限制可以包括不允許頒發許可證的最小安全級別和模組版本清單。 請參閱 [阻止限制訪問受保護內容的DRM客戶端清單](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) 有關用於標識DRM/運行時模組的屬性的詳細資訊。

如果設定了最低安全級別，則客戶端（在電腦令牌中指定）上的版本必須大於或等於指定值。

如果指定了排除的版本清單，並且客戶端的版本與清單中的任何版本標識符匹配，則不允許客戶端使用包含此ModuleRequirements實例的權限。 要使模組與版本資訊匹配，除版本版本外，版本資訊中指定的所有參數必須與模組的值完全匹配。 如果客戶端模組的值小於或等於版本資訊中的值，則版本版本匹配。

在使用特定DRM客戶端或運行時版本報告違規時，內容所有者和內容分發者（運行許可證伺服器）可以配置伺服器在Adobe沒有可用修復的期間拒絕頒發許可證。 可通過 `HandlerConfiguration` 或更改所有策略。 在後一種情況下，您可以維護策略更新清單並使用它檢查策略是否已更新或吊銷。

如果您需要更新版本的Adobe®Flash®播放器/Adobe® AIR®運行時或Adobe內容保護庫（DRM模組），請更新您的策略，如所示 [使用Java API更新策略](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 建立策略更新清單，或在 `HandlerConfiguration` 調用 `HandlerConfiguration.setRuntimeModuleRequirements()` 或 `HandlerConfiguration.setDRMModuleRequirements()`。 當用戶請求啟用這些塊清單的新許可證時，必須先安裝較新的運行時間和庫，然後才能頒發許可證。 有關列出DRM和運行時版本的塊示例，請參見中的示例代碼 [使用Java API更新策略](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md)。
