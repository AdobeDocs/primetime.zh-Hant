---
title: 使用電腦標識符
description: 使用電腦標識符
copied-description: true
exl-id: 61ff9240-0c29-437e-b676-7983e2cc5f7b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 使用電腦標識符{#using-machine-identifiers}

所有Adobe訪問請求（支援FMRMS相容性的請求除外）都包含有關在個性化期間向客戶端頒發的電腦令牌的資訊。 電腦令牌包含電腦ID，該標識符在個性化過程中分配。 使用此標識符可以計算用戶請求許可證或加入域的電腦數。

使用標識符有兩種方法。 的 `getUniqueId()` 方法返回在個性化期間分配給設備的字串。 可以將字串儲存在資料庫中並按標識符進行搜索。 但是，如果用戶重新格式化硬碟並再次個性化，則此標識符將更改。 此標識符在同一電腦上的不同瀏覽器中在Adobe® AIR®和Adobe®Flash®播放器之間也具有不同的值。

要更準確地計算電腦數量，您可以使用 `getBytes()` 儲存整個標識符。 要確定以前是否看到過電腦，請獲取用戶名的所有標識符並調用 `matches()` 檢查是否匹配。 因為 `matches()` 方法必須用於比較由 `MachineId.getBytes`，此選項僅在有少量值可供比較（例如，與特定用戶關聯的電腦）時才實用。
