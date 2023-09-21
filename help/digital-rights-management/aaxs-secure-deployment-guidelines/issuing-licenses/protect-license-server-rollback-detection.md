---
title: 復原偵測
description: 復原偵測
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---

# 復原偵測 {#rollback-detection}

如果您實施Adobe存取時所使用的商業規則要求使用者端維持狀態（例如播放視窗間隔），Adobe強烈建議伺服器追蹤復原計數器，並使用AIR或SWF允許清單。

在使用者端的多數要求中，都會將回覆計數器傳送至伺服器。 如果您的Adobe存取實作不需要復原計數器，則可忽略。 否則，Adobe建議伺服器儲存隨機機器ID （透過取得） `MachineToken.getMachineId().getUniqueId()` — 和資料庫中目前的計數器值。 如需增加和追蹤倒回計數器的詳細資訊，請參閱以下內容中的ClientState： *Adobe存取API參考* 和 *復原偵測* 在 *使用Adobe Access SDK保護內容*.
