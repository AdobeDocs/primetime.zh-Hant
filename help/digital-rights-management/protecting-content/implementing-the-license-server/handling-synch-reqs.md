---
title: 處理同步請求
description: 處理同步請求
copied-description: true
exl-id: b19245e3-19ae-4dd4-9e5e-6956feb91334
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# 處理同步請求 {#handle-synchronization-requests}

如果許可證指定同步要求  [同步要求，](../../protecting-content/introduction/usage-rules/authentication/synchronization.md) 客戶端根據許可證中指定的頻率定期向伺服器發送同步請求。 要啟用同步消息，請設定 `SyncFrequencyRequirements` 在PlayRight中。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，請求URL為「元資料中的許可證伺服器URL:+ &quot; [!DNL /flashaccess/sync/v4]。 否則，請求URL為&quot;元資料中的許可證伺服器URL&quot;+ &quot; [!DNL /flashaccess/sync/v3]&quot;

同步消息用於將客戶端的時間與伺服器的時間同步。 如果許可證嵌入到內容中並且不需要從許可證伺服器中檢索，則同步客戶機的時間對於防止客戶機修改其時鐘以繞過許可證到期非常重要。

同步消息還可用於將客戶端狀態資訊傳送到伺服器( `getClientState()`)進行回滾檢測。

請參閱 [回滾保護](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection)。
