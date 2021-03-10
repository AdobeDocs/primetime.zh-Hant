---
title: 使用電腦標識符
description: 使用電腦標識符
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# 使用電腦標識符{#using-machine-identifiers}

所有Adobe訪問請求（支援FMRMS相容性的請求除外）都包含有關在個性化過程中發送給客戶機的電腦令牌的資訊。 機器Token包含機器ID，這是個人化期間指派的識別碼。 使用此識別碼可計算使用者要求授權或加入網域的電腦數目。

使用識別碼有兩種方式。 `getUniqueId()`方法會在個人化期間傳回指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼進行搜尋。 不過，如果使用者重新格式化硬碟並再次個人化，此識別碼將會變更。 此識別碼在同一部電腦的不同瀏覽器中，Adobe® AIR®和Adobe®Flash®播放器的值也不同。

要更精確地電腦，可以使用`getBytes()`儲存整個標識符。 要確定以前是否看到過該電腦，請獲取用戶名的所有標識符，並調用`matches()`檢查是否匹配。 由於`matches()`方法必須用於比較`MachineId.getBytes`傳回的值，因此只有當有少量值可供比較時（例如，與特定用戶關聯的電腦），此選項才實用。
