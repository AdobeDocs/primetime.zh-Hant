---
title: 使用電腦標識符
description: 使用電腦標識符
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# 使用電腦標識符{#use-machine-identifiers}

所有Adobe PrimetimeDRM請求（支援FMRMS相容性的請求除外）都包括關於在個性化期間已發給客戶機的機器令牌的資訊。 電腦令牌包括電腦ID，該ID是在個性化期間分配的標識符。 您可以使用此標識符來計算用戶已請求許可證或加入域的電腦數。

您可以使用以下標識符：

* 的 `getUniqueId()` 方法返回在個性化期間分配給設備的字串。 可以將字串儲存在資料庫中並按標識符進行搜索。 但是，如果用戶重新格式化硬碟並再次個性化，則此標識符會更改。 此標識符在同一台電腦上的不同瀏覽器中的Adobe AIR和AdobeFlash Player之間也具有不同的值。
* 如果想更準確地計算電腦，可以使用 `getBytes()` 儲存整個標識符。 要確定以前是否看到過電腦，請獲取用戶名的所有標識符並調用 `matches()` 檢查是否匹配。 因為 `matches()` 方法必須用於比較由 `MachineId.getBytes`，此選項僅在有少量值可供比較時才實用；例如，與特定用戶關聯的電腦。

