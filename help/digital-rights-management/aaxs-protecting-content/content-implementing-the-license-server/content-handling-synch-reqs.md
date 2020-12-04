---
seo-title: 處理同步請求
title: 處理同步請求
uuid: 37b2db09-4c09-4216-874b-b570a84569b6
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---


# 處理同步請求{#handling-synchronization-requests}

.如果許可證指定同步要求（[同步要求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization)），則客戶端將根據許可證中指定的頻率定期向伺服器發送同步請求。 要啟用同步消息，請在PlayRight中設定SyncFrequencyRequirements。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL:+ &quot;/flashaccess/sync/v4&quot;。 否則，請求URL是「中繼資料中的授權伺服器URL」+「/flashaccess/sync/v3」

同步消息用於同步客戶端的時間與伺服器的時間。 如果授權內嵌在內容中，而不需要從授權伺服器擷取，同步用戶端的時間對於防止用戶端修改其時鐘以略過授權到期很重要。

同步消息還可用於將客戶端狀態資訊傳送到伺服器(`getClientState()`)以進行回滾檢測。 請參閱[回滾保護](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md)。