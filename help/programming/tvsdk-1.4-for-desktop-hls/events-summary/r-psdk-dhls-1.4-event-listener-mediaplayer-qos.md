---
description: TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算（例如緩衝或搜尋）的事件。
seo-description: TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算（例如緩衝或搜尋）的事件。
seo-title: QoS事件
title: QoS事件
uuid: fd657cf0-c6d4-4e9a-b212-7d09d483cae9
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# QoS事件{#qos-events}

TVSDK會調度服務品質(QoS)事件，以通知您的應用程式可能會影響QoS統計資料的計算（例如緩衝或搜尋）的事件。

要獲得所有QoS相關事件的通知，請向`MediaPlayer`對象註冊以下事件的事件偵聽器：

| 事件 | 意義 |
|---|---|
| BufferEvent。[BUFFERING_END](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 緩衝已完成。 |
| BufferEvent。[BUFFERING_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 緩衝已開始。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 搜尋已完成。 |
| SeekEvent。[SEEK_BEGIN](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 搜尋正在開始。 |
| SeekEvent。[SEEK_POSITION_ADJUSTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK因現行廣告政策而改變搜尋位置。 |

