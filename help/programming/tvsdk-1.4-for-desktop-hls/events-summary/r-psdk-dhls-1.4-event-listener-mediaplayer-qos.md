---
description: TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝或尋道。
title: QoS事件
exl-id: 7de28d00-12e2-4f2a-bb1b-53661e3578a1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# QoS事件{#qos-events}

TVSDK調度服務質量(QoS)事件，以通知您的應用程式可能影響QoS統計資訊計算的事件，如緩衝或尋道。

要獲得所有QoS相關事件的通知，請向 `MediaPlayer` 對象：

| 事件 | 意義 |
|---|---|
| BufferEvent。[緩衝結束](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_END) | 緩衝已完成。 |
| BufferEvent。[緩衝開始](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/BufferEvent.html#BUFFERING_BEGIN) | 緩衝已啟動。 |
| SeekEvent。[SEEK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_END) | 尋找完成。 |
| SeekEvent。[查找開始](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_BEGIN) | 尋找正在開始。 |
| SeekEvent。[查找位置已調整](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/SeekEvent.html#SEEK_POSITION_ADJUSTED) | TVSDK由於當前廣告策略而改變了查找位置。 |
