---
title: 重放保護
description: 重放保護
copied-description: true
exl-id: dfb6d615-07d2-4303-82cc-10cfee4bb387
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 重放保護{#replay-protection}

對於重播保護，通過調用來檢查消息標識符最近是否已被看到可能是謹慎的 `RequestMessageBase.getMessageId()`。 如果是，則攻擊者可能正嘗試重播請求，應拒絕該請求。 為了檢測重播嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取清單檢查每個傳入請求。 要限制消息標識符需要儲存的時間，請調用 `HandlerConfiguration.setTimestampTolerance()`。 如果設定了此屬性，則SDK將拒絕任何帶有超過指定秒數的時間戳的請求。
