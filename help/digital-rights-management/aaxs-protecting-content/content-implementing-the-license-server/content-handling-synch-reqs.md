---
title: 處理同步請求
description: 處理同步請求
copied-description: true
exl-id: bbfc6096-72df-4597-96b3-8f67a640ea8f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 處理同步請求{#handling-synchronization-requests}

. 如果許可證指定同步要求([同步要求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization))，客戶端將根據許可證中指定的頻率定期向伺服器發送同步請求。 要啟用同步消息，請在PlayRight中設定SyncFrequencyRequirements。

* 請求處理程式類為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求消息類為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客戶端和伺服器都支援協定版本5，請求URL為「元資料中的許可證伺服器URL:+ &quot;/flashaccess/sync/v4&quot;。 否則，請求URL為「元資料中的許可證伺服器URL」+「/flashaccess/sync/v3」

同步消息用於將客戶端的時間與伺服器的時間同步。 如果許可證嵌入到內容中並且不需要從許可證伺服器中檢索，則同步客戶機的時間對於防止客戶機修改其時鐘以繞過許可證到期非常重要。

同步消息還可用於將客戶端狀態資訊傳送到伺服器( `getClientState()`)進行回滾檢測。 請參閱 [回滾保護](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md)。
