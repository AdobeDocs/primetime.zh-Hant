---
title: 處理同步處理要求
description: 處理同步處理要求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 處理同步處理要求{#handling-synchronization-requests}

. 如果授權指定同步化需求([同步化需求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization))，則使用者端會根據授權中指定的頻率，定期傳送同步處理要求給伺服器。 若要啟用同步化訊息，請在PlayRight中設定SyncFrequencyRequirements。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的授權伺服器URL：+ &quot;/flashaccess/sync/v4」。 否則，請求URL是「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/sync/v3&quot;

同步化訊息可用來將使用者端的時間與伺服器的時間同步化。 如果授權內嵌於內容中，且不需要從授權伺服器擷取，同步使用者端的時間非常重要，以防止使用者端修改其時鐘，以略過授權到期。

同步化訊息也可用來將使用者端狀態資訊傳送到伺服器( `getClientState()`)進行回覆偵測。 另請參閱 [復原保護](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
