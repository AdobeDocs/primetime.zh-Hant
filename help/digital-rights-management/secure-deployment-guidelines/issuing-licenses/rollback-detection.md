---
description: 如果您實作的Adobe Primetime DRM使用需要用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF白名單。
seo-description: 如果您實作的Adobe Primetime DRM使用需要用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF白名單。
seo-title: 回滾檢測
title: 回滾檢測
uuid: f161ed41-488a-478a-b6a8-468cf6d11e89
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# 回滾檢測 {#rollback-detection}

如果您實作的Adobe Primetime DRM使用需要用戶端維持狀態（例如播放視窗間隔）的業務規則，Adobe建議伺服器追蹤回滾計數器，並使用AIR或SWF白名單。

回滾計數器在客戶端發出的大多數請求中都發送到伺服器。 如果您的Primetime DRM實作不需要回滾計數器，則可以忽略它。 否則，Adobe建議伺服器儲存隨機機器ID(使用 [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()))，以及資料庫中的目前計數器值。

有關如何增加和跟蹤回滾計數器的詳細資訊，請參 [閱ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) 和Rollback檢測。