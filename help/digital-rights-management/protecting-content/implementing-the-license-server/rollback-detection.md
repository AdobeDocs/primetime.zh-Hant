---
seo-title: 回滾檢測
title: 回滾檢測
uuid: ec124bac-a1d7-45be-bf09-a99d5eec5042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 回滾檢測 {#rollback-detection}

對於回滾檢測，某些使用規則要求客戶端維護狀態資訊以執行權限。 例如，為了強制播放視窗使用規則，用戶端會儲存使用者首次檢視內容的日期和時間。 此事件會觸發播放視窗的開始。 要安全地強制播放窗口，伺服器需要確保用戶不備份和恢復客戶端狀態，以刪除儲存在客戶端上的播放窗口啟動時間。 伺服器通過跟蹤客戶機回滾計數器的值來執行此操作。

對於每個請求，伺服器通過調用獲取對象， `RequestMessageBase.getClientState()` 然後調用獲取 `ClientState` 客戶 `ClientState.getCounter()` 端狀態計數器的當前值來獲取計數器的值。 伺服器應為每個客戶端儲存此值(用 `MachineId.getUniqueId()` 於標識與回滾計數器值關聯的客戶端)，然後調用 `ClientState.incrementCounter()` 將計數器值增加一。 如果伺服器檢測到計數器值小於伺服器所看到的最後一個值，則客戶端狀態可能已回退。

如需用戶 `ClientState` 端狀態竄改偵測的詳細資訊，請參閱API參考檔案。
