---
title: 處理同步處理要求
description: 處理同步處理要求
copied-description: true
exl-id: bbfc6096-72df-4597-96b3-8f67a640ea8f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# 處理同步處理要求{#handling-synchronization-requests}

. 如果授權指定同步化需求([同步化需求](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-time-based-rules/content-time-based-rules-defining.md#requirements-for-synchronization))，則使用者端會根據授權中指定的頻率，定期傳送同步處理要求至伺服器。 若要啟用同步訊息，請在PlayRight中設定SyncFrequencyRequirements。

* 要求處理常式類別為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationHandler`
* 請求訊息類別為 `com.adobe.flashaccess.sdk.protocol.sync.SynchronizationRequestMessage`
* 如果使用者端和伺服器都支援通訊協定版本5，則請求URL是「中繼資料中的授權伺服器URL： + &quot;/flashaccess/sync/v4」。 否則，請求URL是「中繼資料中的授權伺服器URL」+ &quot;/flashaccess/sync/v3&quot;

同步化訊息可用來將使用者端的時間與伺服器的時間同步。 如果授權內嵌於內容中，且不需要從授權伺服器擷取，同步使用者端的時間非常重要，以防止使用者端修改其時鐘，以略過授權到期。

同步化訊息也可用來將使用者端狀態資訊傳遞給伺服器( `getClientState()`)以進行復原偵測。 另請參閱 [復原保護](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-rollback-detection.md).
