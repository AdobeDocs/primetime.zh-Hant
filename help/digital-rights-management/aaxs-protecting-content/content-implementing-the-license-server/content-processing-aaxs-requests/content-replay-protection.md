---
title: 重放保護
description: 重放保護
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重放保護{#replay-protection}

對於重放保護，通過調用`RequestMessageBase.getMessageId()`檢查消息標識符最近是否已被看到可能是謹慎的。 如果是，攻擊者可能會嘗試重播請求，但請求應被拒絕。 為了檢測重放嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取的清單檢查每個傳入的請求。 要限制消息標識符需要儲存的時間，請調用`HandlerConfiguration.setTimestampTolerance()`。 若已設定此屬性，SDK將拒絕任何包含超過伺服器時間指定秒數之時間戳記的請求。
