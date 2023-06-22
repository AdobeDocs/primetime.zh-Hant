---
description: TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有可能會影響QoS統計資料計算的事件，例如緩衝或搜尋。
title: QoS事件
exl-id: 7de28d00-12e2-4f2a-bb1b-53661e3578a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有可能會影響QoS統計資料計算的事件，例如緩衝或搜尋。

若要接收所有QoS相關事件的通知，請註冊事件接聽程式，使用 `MediaPlayer` 物件，用於下列事件：

| 事件 | 含義 |
|---|---|
| 緩衝事件。[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 緩衝完成。 |
| 緩衝事件。[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 緩衝已開始。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 搜尋已完成。 |
| SeekEvent。[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 搜尋正在開始。 |
| SeekEvent。[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK已因目前的廣告原則而變更搜尋位置。 |
