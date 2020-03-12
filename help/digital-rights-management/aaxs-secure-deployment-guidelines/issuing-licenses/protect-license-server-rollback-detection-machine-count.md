---
seo-title: 核發授權時的機器計數
title: 核發授權時的機器計數
uuid: d57f8b0b-0363-4b26-bd71-76f4abe5b68f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 核發授權時的機器計數{#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。 追蹤機器ID的最強穩方式是將方法傳回的值儲 `MachineId.getBytes()` 存在資料庫中。 當有新請求傳入時，請比較請求中的機器ID與使用的已知機器ID `MachineId.matches()`。

`MachineId.matches()` 執行ID比較，以判斷它們是否代表相同的機器。 只有當有少量機器ID可供比較時，此比較才實用。 例如，如果用戶在其域內允許五台電腦，則可以搜索資料庫以查找與用戶用戶名關聯的電腦ID，並獲取一組要比較的小資料。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>此比較不適用於允許匿名存取的部署。 但是，在 `MachineId.getUniqueID()` 這些情況下，如果使用者從Flash和Adobe AIR®執行階段存取內容，則此ID不會相同，而當使用者重新格式化其硬碟時，此ID將無法存在。

若要進一步了 `MachineToken.getMachineId()`解 `MachineId.matches()`和，請參 *閱Adobe Access API參考*。
