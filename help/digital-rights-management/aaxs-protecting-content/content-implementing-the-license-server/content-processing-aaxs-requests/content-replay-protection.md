---
title: 重播保護
description: 重播保護
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 重播保護{#replay-protection}

針對重播保護，檢查訊息識別碼最近是否透過呼叫顯示可能是審慎的做法 `RequestMessageBase.getMessageId()`. 若是如此，攻擊者可能會嘗試重新執行要求，但應予以拒絕。 若要偵測重播嘗試，伺服器可以儲存最近檢視過的訊息ID清單，並根據快取清單檢查每個傳入要求。 若要限制需要儲存訊息識別碼的時間長度，請呼叫 `HandlerConfiguration.setTimestampTolerance()`. 如果設定此屬性，SDK將會拒絕任何時間戳記超過伺服器時間指定秒數的請求。
