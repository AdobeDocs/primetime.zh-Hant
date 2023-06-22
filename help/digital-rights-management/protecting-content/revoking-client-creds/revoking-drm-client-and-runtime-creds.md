---
title: 撤銷DRM使用者端和執行階段認證
description: 撤銷DRM使用者端和執行階段認證
copied-description: true
exl-id: 3a91a256-ab01-48d8-99f3-854195faae6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 撤銷DRM使用者端和執行階段認證 {#revoking-drm-client-and-runtime-credentials}

DRM/執行階段版本由安全性等級、版本編號和其他屬性（包括作業系統和執行階段）來識別。 若要限制允許的DRM/執行階段版本，請在DRM政策或 `HandlerConfiguration`. 模組限制可能包括最低安全等級和不允許核發授權的模組版本清單。

另請參閱 [封鎖無法存取受保護內容的DRM使用者端清單](../../protecting-content/introduction/usage-rules/runtime-application-restrictions/blocklist-drm-clients.md) 有關用於識別DRM/執行階段模組的屬性的詳細資訊。

如果已設定最低安全性層級，使用者端上的版本（在電腦權杖中指定）必須大於或等於指定的值。

如果指定了排除版本的清單，並且使用者端的版本符合清單中的任何版本識別碼，則不允許使用者端使用包含此ModuleRequirements執行個體的許可權。 為了讓模組符合版本資訊，版本資訊中指定的所有引數（發行版本除外）都必須完全符合模組的值。 如果使用者端模組的值小於或等於版本資訊中的值，則發行版本會相符。

如果報告特定DRM使用者端或執行階段版本發生違規，內容擁有者和內容散發者（執行授權伺服器的人）可以設定伺服器，在Adobe沒有可用的修正期間拒絕簽發授權。 這可以透過以下方式設定： `HandlerConfiguration` 如上所述，或透過變更所有DRM政策來進行。 在後一種情況下，您可以維護DRM政策更新清單，並使用它來檢查DRM政策是否已更新或撤銷。

如果您需要較新版本的AdobeFlash Player/Adobe AIR執行階段或Adobe內容保護程式庫（DRM模組），則需要更新DRM原則。

另請參閱 [使用Java API更新原則](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md).

然後，您需要建立DRM政策更新清單或設定限制 `HandlerConfiguration` 透過叫用 `HandlerConfiguration.setRuntimeModuleRequirements()` 或 `HandlerConfiguration.setDRMModuleRequirements()`. 當使用者請求已啟用指定封鎖清單的新授權時，您必須安裝最新的執行階段和程式庫，才能核發授權。

請參閱中的範常式式碼 [使用Java API更新原則舉例說明列出DRM和執行階段版本的區塊](../../protecting-content/working-policies-overview/updating-policy-using-java-api.md) 以區塊為例，列出DRM和執行階段版本。
