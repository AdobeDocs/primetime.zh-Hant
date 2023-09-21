---
title: 簽發授權時的電腦計數
description: 簽發授權時的電腦計數
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 簽發授權時的電腦計數{#machine-count-when-issuing-licenses}

如果商業規則要求追蹤使用者的電腦數目，則License Server或Domain Server必須儲存與使用者相關聯的電腦ID。 追蹤機器ID最有效的方法是儲存 `MachineId.getBytes()` 資料庫中的方法。 傳入新請求時，請使用將請求中的電腦ID與已知的電腦ID進行比較 `MachineId.matches()`.

`MachineId.matches()` 會執行ID的比較，以判斷它們是否代表同一部電腦。 只有在要比較的機器ID數量較少時，這項比較才切實可行。 例如，如果允許使用者在其網域內使用五台電腦，您可以在資料庫中搜尋與使用者使用者名稱相關聯的電腦ID，並取得一小部分的資料集來進行比較。

>[!NOTE]
>
>此比較不適用於允許匿名存取的部署。 在這種情況下 `MachineId.getUniqueID()` 但是，如果使用者同時從Flash和Adobe AIR®執行階段存取內容，則此ID不會相同；如果使用者重新格式化其硬碟，此ID將無法存留。

若要深入瞭解 `MachineToken.getMachineId()`和 `MachineId.matches()`，請參閱 *Adobe存取API參考*.
