---
title: 核發授權時的機器計數
description: 核發授權時的機器計數
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 核發授權時的機器計數{#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。 追蹤機器ID最穩健的方式是將`MachineId.getBytes()`方法傳回的值儲存在資料庫中。 當有新請求出現時，請使用`MachineId.matches()`比較請求中的機器ID與已知的機器ID。

`MachineId.matches()` 執行ID比較，以判斷它們是否代表相同的機器。此比較只有在有少量機器ID可供比較時才實用。 例如，如果用戶在其域內允許五台電腦，則可以搜索資料庫以查找與用戶用戶名關聯的電腦ID，並獲取一組要比較的小資料。

>[!NOTE]
>
>此比較不適用於允許匿名存取的部署。 但是，在這些情況下，使用者可以使用`MachineId.getUniqueID()`，但是，如果使用者同時從Flash和Adobe AIR®執行階段存取內容，則此ID不相同，如果使用者重新格式化其硬碟，則此ID將無法存留。

若要進一步瞭解`MachineToken.getMachineId()`和`MachineId.matches()`，請參閱&#x200B;*Adobe存取API參考*。
