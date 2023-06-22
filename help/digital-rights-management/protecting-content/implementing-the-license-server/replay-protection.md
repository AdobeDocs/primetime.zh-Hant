---
title: 重播保護
description: 重播保護
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# 重播保護{#replay-protection}

針對重播保護，您可能想要透過呼叫檢查最近是否看到訊息識別碼 `RequestMessageBase.getMessageId()`. 若是如此，攻擊者可能會嘗試重新執行要求，但應予以拒絕。 若要偵測重播嘗試，伺服器可以儲存最近檢視的訊息ID清單，並根據快取清單檢查每個傳入請求。 若要限制需要儲存訊息識別碼的時間長度，請呼叫 `HandlerConfiguration.setTimestampTolerance()`. 若此屬性已設定，則SDK會拒絕任何包含時間戳記超過伺服器時間指定秒數的請求。
