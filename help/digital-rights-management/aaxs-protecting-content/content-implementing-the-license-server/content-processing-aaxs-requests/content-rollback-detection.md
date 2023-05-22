---
title: 回滾檢測
description: 回滾檢測
copied-description: true
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 回滾檢測{#rollback-detection}

對於回滾檢測，某些使用規則要求客戶端維護狀態資訊以執行權限。 例如，要強制實施播放窗口使用規則，客戶端儲存用戶首次開始查看內容的日期和時間。 此事件觸發播放窗口的開始。 為了安全地強制播放窗口，伺服器需要確保用戶沒有備份和恢復客戶端狀態，以便刪除儲存在客戶端上的播放窗口開始時間。 伺服器通過跟蹤客戶端回滾計數器的值來執行此操作。 對於每個請求，伺服器通過調用獲取計數器的值 `RequestMessageBase.getClientState()` 獲取 `ClientState` 對象，然後調用 `ClientState.getCounter()` 獲取客戶端狀態計數器的當前值。 伺服器應為每個客戶端儲存此值(使用 `MachineId.getUniqueId()` 標識與回滾計數器值關聯的客戶端)，然後調用 `ClientState.incrementCounter()` 將計數器值增加1。 如果伺服器檢測到計數器值小於伺服器看到的最後一個值，則客戶端狀態可能已回滾。 有關客戶端狀態篡改檢測的詳細資訊，請參見 `ClientState` API參考文檔。
