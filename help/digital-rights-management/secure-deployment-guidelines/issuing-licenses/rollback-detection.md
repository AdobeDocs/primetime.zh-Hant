---
description: 如果您實作的Adobe PrimetimeDRM使用要求用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF允許清單。
title: 回滾檢測
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 回滾檢測{#rollback-detection}

如果您實作的Adobe PrimetimeDRM使用要求用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在客戶端發出的大多數請求中都發送到伺服器。 如果您的Primetime DRM實作不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存使用[MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())獲取的隨機電腦ID，以及資料庫中的當前計數器值。

有關如何增加和跟蹤回滾計數器的詳細資訊，請參見[ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html)和回滾檢測。