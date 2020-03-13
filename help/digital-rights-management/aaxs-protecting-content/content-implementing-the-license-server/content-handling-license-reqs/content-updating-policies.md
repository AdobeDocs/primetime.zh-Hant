---
seo-title: 更新策略
title: 更新策略
uuid: f6686c8b-bedf-4ec5-a14e-f03326519f89
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 更新策略 {#updating-policies}

如果在內容封裝後更新了策略，請將更新的策略提供給許可證伺服器，以便在發行許可證時使用更新的版本。 如果您的許可證伺服器有權訪問儲存策略的資料庫，則可以從資料庫中檢索更新的策略並調用以 `LicenseRequestMessage.setSelectedPolicy()` 提供新版本的策略。

對於不依賴中央資料庫的授權伺服器，SDK支援「原則更新清單」。 策略更新清單是包含更新策略或已撤銷策略清單的檔案。 更新策略時，生成新的策略更新清單，並定期將清單推送到所有許可證伺服器。 透過設定，將清單傳遞至SDK `HandlerConfiguration.setPolicyUpdateList()`。 如果提供更新清單，SDK會在剖析內容中繼資料時參考此清單。 `ContentInfo.getUpdatedPolicies()` 包含中繼資料中指定之原則的更新版本。

請參 [閱使用策略](../../../aaxs-protecting-content/content-working-with-policies/content-working-with-policies-overview.md) 和 [策略更新清單。](/help/digital-rights-management/protecting-content/working-policies-overview/policy-update-lists/working-with-policy-update-lists.md)
