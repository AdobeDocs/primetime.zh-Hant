---
title: 更新DRM策略
description: 更新DRM策略
copied-description: true
exl-id: 27dc35d2-134c-4b88-9251-c6bb04a48f13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 更新DRM策略 {#updating-drm-policies}

如果在內容打包之後更新DRM策略，則將更新的DRM策略提供給許可證伺服器，以便在發放許可證時可以使用更新的版本。 如果許可證伺服器有權訪問儲存DRM策略的資料庫，則可以從資料庫中檢索更新的DRM策略並調用 `LicenseRequestMessage.setSelectedPolicy()` 提供DRM策略的新版本。

對於不依賴中央資料庫的許可證伺服器，SDK提供對DRM策略更新清單的支援。 DRM策略更新清單是包括更新或撤消的DRM策略清單的檔案。 更新DRM策略時，生成新的DRM策略更新清單並定期將清單推送到所有許可證伺服器。 通過設定將清單傳遞到SDK `HandlerConfiguration.setPolicyUpdateList()`。 如果提供了更新清單，則SDK在解析內容元資料時會參考此清單。 `ContentInfo.getUpdatedPolicies()` 包括元資料中指定的DRM策略的更新版本。

請參閱 [使用DRM策略](../../../protecting-content/working-policies-overview/working-with-policies.md) 和 [DRM策略更新清單](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
