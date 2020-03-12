---
seo-title: 使用電腦標識符
title: 使用電腦標識符
uuid: 2832c158-fade-4bbf-ae89-f95ce9dfc369
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用電腦標識符{#using-machine-identifiers}

所有Adobe Access請求（支援FMRMS相容性的請求除外）都包含個人化期間發送給用戶端之機器Token的相關資訊。 機器Token包含機器ID，這是個人化期間指派的識別碼。 使用此識別碼可計算使用者要求授權或加入網域的電腦數目。

使用識別碼有兩種方式。 該方 `getUniqueId()` 法會在個人化期間傳回指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼進行搜尋。 不過，如果使用者重新格式化硬碟並再次個人化，此識別碼將會變更。 此識別碼在相同機器上的不同瀏覽器中，Adobe® AIR®和Adobe® Flash® Player之間的值也會不同。

若要更精確地電腦，您可使 `getBytes()` 用儲存整個識別碼。 若要判斷之前是否已檢視過電腦，請取得使用者名稱的所有識別碼，並呼叫以 `matches()` 檢查是否相符。 由於必 `matches()``MachineId.getBytes`須使用方法來比較傳回的值，因此只有當有少量值可供比較時（例如，與特定使用者相關聯的電腦），此選項才實用。
