---
title: 復原偵測
description: 復原偵測
copied-description: true
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 復原偵測{#rollback-detection}

對於復原偵測，某些使用規則會要求使用者端維護執行許可權的狀態資訊。 例如，若要強制執行播放視窗使用規則，使用者端會儲存使用者首次開始檢視內容的日期和時間。 此事件會觸發播放視窗的開始。 為了安全地強制執行播放視窗，伺服器需要確保使用者沒有備份及還原使用者端狀態，以便移除儲存在使用者端上的播放視窗開始時間。 伺服器透過追蹤使用者端復原計數器的值來執行此操作。 伺服器會針對每個要求呼叫，以取得計數器的值 `RequestMessageBase.getClientState()` 以取得 `ClientState` 物件，然後呼叫 `ClientState.getCounter()` 以取得使用者端狀態計數器的目前值。 伺服器應該為每個使用者端儲存此值(使用 `MachineId.getUniqueId()` 以識別與倒回計數器值相關聯的使用者端)，然後呼叫 `ClientState.incrementCounter()` 將計數器值增加1。 如果伺服器偵測到計數器值小於伺服器看到的最後一個值，則使用者端狀態可能已復原。 如需使用者端狀態篡改偵測的詳細資訊，請參閱 `ClientState` API參考檔案。
