---
seo-title: 重放保護
title: 重放保護
uuid: c737998a-9c33-48b4-b741-91106697d71f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 重放保護{#replay-protection}

對於重放保護，您可能希望通過調用來檢查最近是否看到消息標識符 `RequestMessageBase.getMessageId()`。 如果是，攻擊者可能會嘗試重播請求，但請求應被拒絕。 為了檢測重放嘗試，伺服器可以儲存最近看到的消息ID的清單，並根據快取的清單檢查每個傳入的請求。 要限制消息標識符需要儲存的時間，請調用 `HandlerConfiguration.setTimestampTolerance()`。 若已設定此屬性，SDK會拒絕任何攜帶時間戳記超過伺服器時間指定秒數的請求。
