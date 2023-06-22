---
description: 如果您的Adobe Primetime DRM實作使用要求使用者端維持狀態的商業規則（例如播放視窗間隔），Adobe建議伺服器追蹤倒回計數器，並使用AIR或SWF允許清單。
title: 復原偵測
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# 復原偵測 {#rollback-detection}

如果您的Adobe Primetime DRM實作使用要求使用者端維持狀態的商業規則（例如播放視窗間隔），Adobe建議伺服器追蹤倒回計數器，並使用AIR或SWF允許清單。

在使用者端的大部分要求中，都會將回覆計數器傳送至伺服器。 如果您的Primetime DRM實作不需要倒回計數器，則可以忽略。 否則，Adobe建議伺服器儲存隨機機器ID，此ID是使用取得 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId())，以及資料庫中目前的計數器值。

如需如何遞增及追蹤倒回計數器的詳細資訊，請參閱 [使用者端狀態](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和復原偵測。