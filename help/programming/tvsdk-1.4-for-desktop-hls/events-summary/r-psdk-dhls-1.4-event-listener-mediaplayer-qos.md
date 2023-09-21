---
description: TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝或搜尋。
title: QoS事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK會傳送服務品質(QoS)事件，通知您的應用程式有關可能影響QoS統計資料計算的事件，例如緩衝或搜尋。

若要接收所有QoS相關事件的通知，請以註冊事件接聽程式 `MediaPlayer` 物件，用於下列事件：

| 事件 | 含義 |
|---|---|
| 緩衝區事件。[緩衝結束](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 緩衝完成。 |
| 緩衝區事件。[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 緩衝已開始。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 搜尋已完成。 |
| SeekEvent。[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 正在開始搜尋。 |
| SeekEvent。[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK已因目前廣告原則而變更搜尋位置。 |
