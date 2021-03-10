---
title: 更新DRM策略
description: 更新DRM策略
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 更新DRM策略{#updating-drm-policies}

如果在內容打包之後更新了DRM策略，則將更新的DRM策略提供給許可證伺服器，以便在發放許可證時可以使用更新的版本。 如果許可伺服器可以訪問儲存DRM策略的資料庫，則可以從資料庫中檢索更新的DRM策略，並調用`LicenseRequestMessage.setSelectedPolicy()`來提供DRM策略的新版本。

對於不依賴中央資料庫的授權伺服器，SDK支援DRM原則更新清單。 DRM策略更新清單是包括更新或撤銷的DRM策略的清單的檔案。 更新DRM策略時，生成新的DRM策略更新清單，並定期將清單推送到所有許可證伺服器。 設定`HandlerConfiguration.setPolicyUpdateList()`，將清單傳遞至SDK。 如果提供更新清單，SDK會在分析內容中繼資料時參考此清單。 `ContentInfo.getUpdatedPolicies()` 包括元資料中指定的DRM策略的更新版本。

請參閱[使用DRM策略](../../../protecting-content/working-policies-overview/working-with-policies.md)和[DRM策略更新清單](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)