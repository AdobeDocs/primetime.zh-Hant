---
title: 回滾檢測
description: 回滾檢測
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# 回滾檢測{#rollback-detection}

對於回滾檢測，某些使用規則要求客戶端維護狀態資訊以執行權限。 例如，為了強制播放視窗使用規則，用戶端會儲存使用者首次檢視內容的日期和時間。 此事件會觸發播放視窗的開始。 為了安全地強制播放窗口，伺服器需要確保用戶不備份和恢復客戶端狀態，以便刪除儲存在客戶端上的播放窗口開始時間。 伺服器通過跟蹤客戶機回滾計數器的值來執行此操作。 對於每個請求，伺服器通過調用`RequestMessageBase.getClientState()`獲取`ClientState`對象，然後調用`ClientState.getCounter()`獲取客戶端狀態計數器的當前值來獲取計數器的值。 伺服器應為每個客戶機儲存此值（使用`MachineId.getUniqueId()`標識與回滾計數器值關聯的客戶機），然後調用`ClientState.incrementCounter()`將計數器值增加一。 如果伺服器檢測到計數器值小於伺服器所看到的最後一個值，則客戶端狀態可能已回退。 如需用戶端狀態竄改偵測的詳細資訊，請參閱`ClientState` API參考檔案。
