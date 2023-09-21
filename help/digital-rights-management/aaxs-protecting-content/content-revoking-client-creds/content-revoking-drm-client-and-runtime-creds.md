---
title: 撤銷DRM使用者端和執行階段認證
description: 撤銷DRM使用者端和執行階段認證
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 撤銷DRM使用者端和執行階段認證{#revoking-drm-client-and-runtime-credentials}

DRM/Runtime版本由安全性等級、版本編號和其他屬性（包括OS和執行階段）來識別。 若要限制允許的DRM/執行階段版本，請在原則或 `HandlerConfiguration`. 模組限制可能包括最低安全性等級以及不允許簽發授權的模組版本清單。 另請參閱 [封鎖DRM使用者端清單，限制其存取受保護的內容](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-runtime-application-restrictions/content-blocklist-drm-clients.md) 有關用於識別DRM/執行階段模組的屬性的詳細資訊。

如果已設定最低安全性等級，使用者端上的版本（在電腦權杖中指定）必須大於或等於指定的值。

如果指定了排除版本的清單，並且使用者端的版本符合清單中的任何版本識別碼，則不允許使用者端使用包含此ModuleRequirements執行個體的許可權。 若要讓模組符合版本資訊，版本資訊中指定的所有引數（發行版本除外）都必須完全符合模組的值。 如果使用者端模組的值小於或等於版本資訊中的值，則發行版本會相符。

如果報告特定DRM使用者端或執行階段版本發生違規，內容擁有者和內容散發者（執行授權伺服器的人）可以設定伺服器，在Adobe沒有可用修正的期間拒絕簽發授權。 這可透過進行設定 `HandlerConfiguration` 如上所述，或變更所有原則。 在後一種情況下，您可以維護原則更新清單，並使用它來檢查原則是否已更新或撤銷。

如果您需要較新版本的Adobe®Flash®播放器/Adobe® AIR®執行階段或Adobe內容保護程式庫（DRM模組），請更新您的原則，如所示 [使用Java API更新原則](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md) 並建立原則更新清單，或設定限制 `HandlerConfiguration` 透過叫用 `HandlerConfiguration.setRuntimeModuleRequirements()` 或 `HandlerConfiguration.setDRMModuleRequirements()`. 當使用者請求新授權並啟用這些封鎖清單時，必須先安裝更新的執行階段和程式庫，然後才能頒發授權。 如需列示DRM和執行階段版本的區塊範例，請參閱下列範常式式碼： [使用Java API更新原則](../../aaxs-protecting-content/content-working-with-policies/content-updating-policy-using-java-api.md).
