---
title: 頒發許可證時的電腦計數
description: 頒發許可證時的電腦計數
copied-description: true
exl-id: de052e98-8ae3-4e12-8f77-787293edda39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 頒發許可證時的電腦計數{#machine-count-when-issuing-licenses}

如果業務規則要求跟蹤用戶的電腦數，則許可證伺服器或域伺服器必須儲存與用戶關聯的電腦ID。 跟蹤電腦ID的最穩健方法是儲存由 `MachineId.getBytes()` 中的設定。 當新請求出現時，將請求中的電腦ID與使用的已知電腦ID進行比較 `MachineId.matches()`。

`MachineId.matches()` 執行ID的比較以確定它們是否代表同一台電腦。 只有與之比較的電腦ID數量很少時，此比較才實用。 例如，如果允許用戶在其域內使用五台電腦，則可以在資料庫中搜索與用戶用戶名關聯的電腦ID，並獲取一小組資料進行比較。

>[!NOTE]
>
>此比較對於允許匿名訪問的部署來說不實用。 在這種情況下 `MachineId.getUniqueID()` 但是，如果用戶從Flash和Adobe AIR®運行時訪問內容，則此ID將不相同，如果用戶重新格式化其硬碟，則此ID將無法生存。

瞭解有關 `MachineToken.getMachineId()`和 `MachineId.matches()`，請參見 *Adobe訪問API參考*。
