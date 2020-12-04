---
seo-title: 處理同步請求
title: 處理同步請求
uuid: e2623afb-7a57-402d-a8a1-07bcf6324d41
translation-type: tm+mt
source-git-commit: eed2ed2512c2c462cd43637d83d80bf9a5c0d490
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# 處理同步請求{#handle-synchronization-requests}

如果許可證指定同步要求[同步要求，則](../../protecting-content/introduction/usage-rules/authentication/synchronization.md)客戶端根據許可證中指定的頻率定期向伺服器發送同步請求。 要啟用同步消息，請在PlayRight中設定`SyncFrequencyRequirements`。

* 請求處理常式類別為`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求消息類為`com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果客戶端和伺服器都支援第5版協定，請求URL為「元資料中的許可證伺服器URL:+ &quot; [!DNL /flashaccess/sync/v4]&quot;。 否則，請求URL是「中繼資料中的授權伺服器URL」+「 [!DNL /flashaccess/sync/v3]」

同步消息用於同步客戶端的時間與伺服器的時間。 如果授權內嵌在內容中，而不需要從授權伺服器擷取，同步用戶端的時間對於防止用戶端修改其時鐘以略過授權到期很重要。

同步消息還可用於將客戶端狀態資訊傳送到伺服器(`getClientState()`)以進行回滾檢測。

請參閱[回滾保護](../../protecting-content/implementing-the-license-server/processing-drm-requests.md#rollback-detection)。
