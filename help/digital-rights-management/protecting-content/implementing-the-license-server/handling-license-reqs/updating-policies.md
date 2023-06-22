---
title: 更新DRM原則
description: 更新DRM原則
copied-description: true
exl-id: 27dc35d2-134c-4b88-9251-c6bb04a48f13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 更新DRM原則 {#updating-drm-policies}

如果在封裝內容後更新DRM原則，請將更新的DRM原則提供給許可證伺服器，以便在發行許可證時可以使用更新的版本。 如果授權伺服器可存取用來儲存DRM原則的資料庫，您可以從資料庫擷取更新的DRM原則並呼叫 `LicenseRequestMessage.setSelectedPolicy()` 提供新版的DRM原則。

對於不依賴中央資料庫的授權伺服器，SDK會提供DRM原則更新清單的支援。 DRM政策更新清單是包含已更新或撤銷DRM政策清單的檔案。 更新DRM原則時，產生新的DRM原則更新清單，並定期將該清單推送到所有授權伺服器。 透過設定將清單傳遞至SDK `HandlerConfiguration.setPolicyUpdateList()`. 如果提供更新清單，SDK在剖析內容中繼資料時會參考此清單。 `ContentInfo.getUpdatedPolicies()` 包括中繼資料中所指定的DRM原則的更新版本。

另請參閱 [使用DRM原則](../../../protecting-content/working-policies-overview/working-with-policies.md) 和 [DRM原則更新清單](../../../protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
