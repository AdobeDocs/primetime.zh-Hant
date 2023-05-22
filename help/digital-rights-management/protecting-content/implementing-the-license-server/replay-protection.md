---
title: 重放保護
description: 重放保護
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重放保護{#replay-protection}

對於重播保護，您可能需要通過調用來檢查最近是否看到消息標識符 `RequestMessageBase.getMessageId()`。 如果是，則攻擊者可能正嘗試重播請求，應拒絕該請求。 為了檢測重播嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取清單檢查每個傳入請求。 要限制消息標識符需要儲存的時間，請調用 `HandlerConfiguration.setTimestampTolerance()`。 如果設定了此屬性，則SDK會拒絕任何帶有超過指定秒數的時間戳的伺服器時間請求。
