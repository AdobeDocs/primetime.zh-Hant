---
title: 回滾檢測
description: 回滾檢測
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 回滾檢測{#rollback-detection}

如果您的「Adobe存取」實作使用要求用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe強烈建議伺服器追蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在客戶端發出的大多數請求中都發送到伺服器。 如果您的Adobe訪問實施不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器將使用`MachineToken.getMachineId().getUniqueId()`獲取的隨機電腦ID和資料庫中的當前計數器值儲存起來。 有關增加和跟蹤回滾計數器的詳細資訊，請參閱&#x200B;*Adobe訪問API參考*&#x200B;和&#x200B;*使用Adobe訪問SDK保護內容*&#x200B;中的&#x200B;*回滾檢測*&#x200B;中的ClientState。
