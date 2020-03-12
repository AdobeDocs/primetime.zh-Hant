---
seo-title: 使用機器識別碼
title: 使用機器識別碼
uuid: 14eee414-62f1-4a9d-84bd-689ca2271d19
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用機器識別碼{#use-machine-identifiers}

所有Adobe Primetime DRM請求（支援FMRMS相容性的請求除外）都包含在個人化期間發送給用戶端之機器Token的相關資訊。 機器Token包含機器ID，此為在個人化期間指派的識別碼。 您可以使用此識別碼來計算使用者要求授權或加入網域的電腦數目。

您可以使用以下識別碼：

* 該方 `getUniqueId()` 法返回在個人化期間指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼進行搜尋。 不過，如果使用者重新格式化硬碟並再次個人化，此識別碼會變更。 此識別碼在相同機器上，Adobe AIR和Adobe Flash Player在不同瀏覽器上的值也不同。
* 如果您想要更精確地電腦，可以使 `getBytes()` 用儲存整個標識符。 若要判斷之前是否已檢視過電腦，請取得使用者名稱的所有識別碼，並呼叫以 `matches()` 檢查是否相符。 由於必 `matches()` 須使用方法來比較傳回的值，因此 `MachineId.getBytes`，只有少數值可供比較時，此選項才實用；例如，與特定用戶關聯的電腦。

