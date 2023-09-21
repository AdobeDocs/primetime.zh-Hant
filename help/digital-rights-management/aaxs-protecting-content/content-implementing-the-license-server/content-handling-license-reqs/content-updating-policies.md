---
title: 更新原則
description: 更新原則
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 更新原則 {#updating-policies}

如果原則在內容封裝後更新，請將更新的原則提供給授權伺服器，以便在發行授權時可以使用更新的版本。 如果您的授權伺服器可存取資料庫以儲存原則，您可以從資料庫擷取更新的原則，並呼叫 `LicenseRequestMessage.setSelectedPolicy()` 提供原則的新版本。

對於不依賴中央資料庫的授權伺服器，SDK提供原則更新清單支援。 原則更新清單是包含已更新或已撤銷原則清單的檔案。 更新原則時，產生新的原則更新清單，並定期將清單推送到所有授權伺服器。 透過設定將清單傳遞至SDK `HandlerConfiguration.setPolicyUpdateList()`. 如果提供更新清單，SDK在剖析內容中繼資料時會參考此清單。 `ContentInfo.getUpdatedPolicies()` 包含中繼資料中所指定原則的更新版本。

另請參閱 [使用原則](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) 和 [原則更新清單。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
