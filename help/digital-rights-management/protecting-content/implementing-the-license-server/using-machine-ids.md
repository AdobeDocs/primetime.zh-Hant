---
title: 使用機器識別碼
description: 使用機器識別碼
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 使用電腦標識符{#use-machine-identifiers}

所有Adobe PrimetimeDRM請求（支援FMRMS相容性的請求除外）都包括關於在個人化期間發送給客戶機的機器令牌的資訊。 機器Token包含機器ID，此為在個人化期間指派的識別碼。 您可以使用此識別碼來計算使用者要求授權或加入網域的電腦數目。

您可以使用以下識別碼：

* `getUniqueId()`方法會傳回在個別化期間指派給裝置的字串。 您可以將字串儲存在資料庫中，並依識別碼進行搜尋。 不過，如果使用者重新格式化硬碟並再次個人化，此識別碼會變更。 此識別碼在同一部機器上，Adobe AIR和AdobeFlash Player在不同瀏覽器中的值也不同。
* 如果您想要更精確地電腦，可以使用`getBytes()`來儲存整個標識符。 要確定以前是否看到過該電腦，請獲取用戶名的所有標識符，並調用`matches()`檢查是否匹配。 由於`matches()`方法必須用來比較`MachineId.getBytes`傳回的值，因此只有在有少量值可供比較時，此選項才實用；例如，與特定用戶關聯的電腦。

