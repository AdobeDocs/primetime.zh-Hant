---
description: 如果您的Adobe PrimetimeDRM實施使用要求客戶端維護狀態的業務規則（例如，回放窗口間隔）,Adobe建議伺服器跟蹤回滾計數器，並使用AIR或SWF允許清單。
title: 回滾檢測
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 回滾檢測 {#rollback-detection}

如果您的Adobe PrimetimeDRM實施使用要求客戶端維護狀態的業務規則（例如，回放窗口間隔）,Adobe建議伺服器跟蹤回滾計數器，並使用AIR或SWF允許清單。

回滾計數器在來自客戶端的大多數請求中都發送到伺服器。 如果您的Mighine DRM實現不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存隨機電腦ID，該ID是使用 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及資料庫中的當前計數器值。

有關如何遞增和跟蹤回退計數器的詳細資訊，請參見 [客戶端狀態](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和回滾檢測。