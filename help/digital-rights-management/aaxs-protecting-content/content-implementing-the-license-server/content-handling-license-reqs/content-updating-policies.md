---
title: 更新策略
description: 更新策略
copied-description: true
exl-id: 0ea8d03b-68dd-415e-a75b-fd439bf858b6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 更新策略 {#updating-policies}

如果策略在內容打包後被更新，請將更新的策略提供給許可證伺服器，以便在頒發許可證時可以使用更新的版本。 如果您的許可證伺服器有權訪問用於儲存策略的資料庫，則可以從資料庫中檢索更新的策略並調用 `LicenseRequestMessage.setSelectedPolicy()` 提供策略的新版本。

對於不依賴中央資料庫的許可證伺服器，SDK支援策略更新清單。 策略更新清單是包含已更新或已撤消策略清單的檔案。 更新策略時，生成新的策略更新清單，並定期將清單推送到所有許可證伺服器。 通過設定將清單傳遞到SDK `HandlerConfiguration.setPolicyUpdateList()`。 如果提供了更新清單，則SDK在分析內容元資料時會參考此清單。 `ContentInfo.getUpdatedPolicies()` 包含元資料中指定的策略的更新版本。

請參閱 [使用策略](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) 和 [策略更新清單。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
